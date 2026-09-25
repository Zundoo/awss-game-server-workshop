
### Vietnamese — `5.6 Load Balancing`

```markdown
---
title : "Load Balancing"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 5.6 </b> "
---

## Cấu hình kiến trúc Application Load Balancer

Phần này trình bày cấu hình kiến trúc **Application Load Balancer (ALB)** được sử dụng để cung cấp khả năng truy cập từ bên ngoài đến Real-time Game Server.

Quy trình bao gồm tạo **Target Group** cho các ECS Fargate Task, triển khai **Internet-facing Application Load Balancer** và kiểm tra trạng thái Health Check của các Game Server Target đã đăng ký.

## Tổng quan triển khai

1. **Target Group**: Cấu hình định tuyến đến các Game Server container đang chạy trên port `8080`.

2. **Application Load Balancer**: Triển khai ALB hướng Internet bên trong Public Subnets để tiếp nhận các kết nối từ Client.

3. **Health Check**: Kiểm tra ALB có thể kết nối và theo dõi trạng thái hoạt động của các Game Server Task.

## Kiến trúc Load Balancing

```text
                         Internet
                            │
                            │ HTTP :80
                            ▼
                ┌───────────────────────┐
                │   Application Load    │
                │      Balancer         │
                │    alb-game-server    │
                └───────────┬───────────┘
                            │
                            │ Forward
                            ▼
                ┌───────────────────────┐
                │    tg-game-server     │
                │     Target Group      │
                └───────────┬───────────┘
                            │
                            │ HTTP :8080
                            ▼
                ┌───────────────────────┐
                │    ECS Fargate Task   │
                │      Game Server      │
                └───────────────────────┘