
### Vietnamese — `5.3.2 Docker Image`

```markdown
---
title : "Docker Image"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.3.2 </b> "
---

## Xây dựng cấu hình Dockerfile

Ứng dụng Game Server được đóng gói bằng **Dockerfile** với cấu hình nhẹ, nhằm giảm mức sử dụng bộ nhớ của container và cải thiện thời gian khởi động ứng dụng.

Tạo một file có tên `Dockerfile` tại thư mục gốc của project Game Server:

```dockerfile
# Sử dụng Node.js Alpine image nhẹ
FROM node:18-alpine

# Thiết lập thư mục làm việc bên trong container
WORKDIR /app

# Copy các file dependency và cài đặt production dependencies
COPY package*.json ./

RUN npm install --only=production

# Copy toàn bộ source code của ứng dụng
COPY . .

# Expose port mạng của ứng dụng
EXPOSE 8080

# Khai báo command mặc định để chạy ứng dụng
CMD ["node", "server.js"]