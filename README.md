# Open5GS bằng Docker

## 1. Tạo gateway giao tiếp
Thêm gateway có ip là 20.0.0.1
```
docker network create --gateway 20.0.0.1 --subnet 20.0.0.0/24 4g
```
Kiểm tra network cho Docker bằng lệnh
```
docker network ls
```

## 2. Pull các image từ Docker Hub
Docker của phần User Plane:
```
docker pull maduc238/open5gs:user-plane
```
Docker của phần Control Plane:
```
docker pull maduc238/open5gs:control-plane 
```

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

## 4. Chạy các Container và config chúng
### 4.1. Phần User Plane:
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
### 4.2. Phần Control Plane:
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
Truy cập địa chỉ [20.0.0.2:3000](20.0.0.2:3000)
Tên đăng nhập: `admin`
Mật khẩu: `1423`

## 5. Công việc thực hiện:
Máy chủ Docker: wireshark bắt các gói 20.0.0.1 trong interface mới tạo của docker
```
sudo wireshark
```
Các máy container: dùng tcpdump bắt các gói trong interface lo
```
tcp
```
