# Open5GS bằng Docker

## I. Tạo gateway giao tiếp

Thêm gateway có ip là 20.0.0.1
```
docker network create --gateway 20.0.0.1 --subnet 20.0.0.0/24 4g
docker network ls
```
