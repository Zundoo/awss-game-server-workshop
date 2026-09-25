---
title: "4.2.2. Docker Image"
weight: 422
---

# 4.2.2. Viết file cấu hình đóng gói Docker Image

Ứng dụng Game Server được đóng gói thông qua cấu trúc file thiết kế **Dockerfile** tối ưu hóa hiệu năng và dung lượng bộ nhớ:

```dockerfile
# Sử dụng base image phiên bản Node.js rút gọn siêu nhẹ
FROM node:18-alpine

# Thiết lập thư mục làm việc bên trong container
WORKDIR /app

# Sao chép các file quản lý thư viện và thực hiện cài đặt
COPY package*.json ./
RUN npm install --only=production

# Sao chép toàn bộ mã nguồn ứng dụng vào container
COPY . .

# Khai báo cổng lắng nghe của container dịch vụ
EXPOSE 8080

# Lệnh khởi chạy chính thức khi container khởi động
CMD ["node", "server.js"]
```
