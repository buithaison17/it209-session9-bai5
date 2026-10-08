# Bài 5: Khởi chạy dịch vụ đơn giản với Docker Compose

## Mô tả
Dùng Docker Compose (CLI v2) để quản lý một dịch vụ web Nginx thay cho lệnh `docker run`.

## Cấu trúc thư mục
```
homework/session_09/ex5/
├── docker-compose.yml
└── README.md
```

## docker-compose.yml
```yaml
services:
  web:
    image: nginx:alpine
    ports:
      - "8082:80"
```

- `services.web`: khai báo một dịch vụ tên `web`.
- `image: nginx:alpine`: dùng image Nginx bản Alpine.
- `ports: "8082:80"`: ánh xạ cổng 8082 của máy host tới cổng 80 trong container.

> Lưu ý: file YAML thụt lề bằng 2 dấu cách, không dùng Tab.

## Cách chạy

```bash
# 1. Khởi chạy dịch vụ (chạy nền)
docker compose up -d

# 2. Kiểm tra trạng thái
docker compose ps

# 3. Gọi thử dịch vụ
curl http://localhost:8082

# 4. Hạ dịch vụ xuống
docker compose down
```

## Kết quả mong đợi
- `docker compose ps` hiển thị service `web` ở trạng thái `running`, cổng `0.0.0.0:8082->80/tcp`.
- `curl` trả về trang chào mừng của Nginx:
```
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
...
```
- `docker compose down` dừng và xóa container cùng network do Compose tạo ra.
