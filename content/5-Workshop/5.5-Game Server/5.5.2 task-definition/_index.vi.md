---
title: "4.4.2. Task Definition"
weight: 442
---

# 4.4.2. Định nghĩa cấu hình Task Definition

*   **Mục tiêu**: Tạo một bản thiết kế (Blueprint) định nghĩa tài nguyên phần cứng và Image Docker cần dùng để khởi chạy Game Server.
*   **Thông số cấu hình cốt lõi**:
    1. **Task definition family**: `game-server-task`
    2. **Launch type**: `AWS Fargate`
    3. **Task size**: CPU = `0.25 vCPU`, Memory = `0.5 GB` (Cấu hình tối thiểu để tiết kiệm chi phí).
    4. **Container details**:
        * **Name**: `game-server`
        * **Image URI**: Nhập đường dẫn ECR của bạn (Ví dụ: `://amazonaws.com`).
        * **Port mappings**: Container Port = `8080`, Protocol = `TCP`.
    5. **Environment variables**: Truyền các biến cấu hình kết nối Redis:
        * `REDIS_HOST` = `://amazonaws.com`
        * `REDIS_PORT` = `6379`
        * `REDIS_TLS` = `true`

![Cấu hình Container và Biến môi trường trong Task Definition](/images/4.4.2-task-definition.png)
