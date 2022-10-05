# Open5GS bằng Docker

### Mục lục

[1. Tạo gateway giao tiếp](#nung)

[2. Pull các image từ Docker Hub](#slong)

[3. Docker Run các image vừa nhận được](#slam)

[4. Chạy các Container và config chúng](#sli)
- [4.1. Phần User Plane](#slinung)
- [4.2. Phần Control Plane](#slislong)

[5. Công việc thực hiện](#ha)

<a name="nung"></a>
## 1. Tạo gateway giao tiếp
Thêm gateway có ip là 20.0.0.1
```
docker network create --gateway 20.0.0.1 --subnet 20.0.0.0/24 4g
```
Sơ đồ cấu hình:
```
-------------           -----------------------             -----------------------   if: ogs-internet 172.17.0.23/16
|  eNodeB   |           |  EPC Control Plane  |             |    EPC User Plane   |------------------------------------- INTERNET
-------------           -----------------------             -----------------------
      |                            |                                    |
      |                            |  20.0.0.2,3,4                      |   20.0.0.5,6                  if: 20.0.0.0/24
    --------------------------------------------------------------------------------------------------------------------
```
Kiểm tra network cho Docker bằng lệnh
```
docker network ls
```

<a name="slong"></a>
## 2. Pull các image từ Docker Hub
Docker của phần User Plane:
```
docker pull maduc238/open5gs:user-plane
```
Docker của phần Control Plane:
```
docker pull maduc238/open5gs:control-plane 
```

<a name="slam"></a>
## 3. Docker Run các image vừa nhận được
Lưu ý: Hai Docker chạy trên 2 terminal khác nhau

User Plane:
```
docker run --name open5gs-u -d -t --cap-add=NET_ADMIN --cap-add=NET_RAW --net 4g --ip 20.0.0.5 --device /dev/net/tun maduc238/open5gs:user-plane
```
Control Plane:
```
docker run --name open5gs-c -d -t --cap-add=NET_ADMIN --cap-add=NET_RAW --net 4g --ip 20.0.0.2 --device /dev/net/tun maduc238/open5gs:control-plane
```

<a name="sli"></a>
## 4. Chạy các Container và config chúng
<a name="slinung"></a>
### 4.1. Phần User Plane
Cấu hình mạng:
```
docker exec -it open5gs-u bash 
ip addr add 20.0.0.6/24 dev eth0 
ip tuntap add name ogs-internet mode tun  
ip addr add 172.17.0.23/16 dev ogs-internet  
ip link set ogs-internet up  
iptables -t nat -A POSTROUTING -s 172.17.0.23 ! -o ogs-internet -j MASQUERADE 
```
Chạy Container:
```
cd home/open5gs 
./run.sh 
```
<a name="slislong"></a>
### 4.2. Phần Control Plane
Cấu hình mạng:
```
docker exec -it open5gs-c bash 
ip addr add 20.0.0.3/24 dev eth0 
ip addr add 20.0.0.4/24 dev eth0 
```
Chạy Container:
```
cd open5gs
./run4g_cp.sh
```
Vào phần web UI:
Truy cập địa chỉ [20.0.0.2:3000](http://20.0.0.2:3000)
Tên đăng nhập: `admin`
Mật khẩu: `1423`

<a name="ha"></a>
## 5. Công việc thực hiện
Lấy id của subnet 4g tạo lúc đầu
```
docker network ls | grep 4g
```
Máy chủ Docker: capture các gói tin chuyển qua interface mới tạo của docker có dạng br-id
```
sudo wireshark
```
Các máy container: dùng tcpdump bắt các gói trong interface loopback
```
tcpdump -i lo -s 65535 -w loopback.pcap
```
