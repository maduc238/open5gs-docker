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

