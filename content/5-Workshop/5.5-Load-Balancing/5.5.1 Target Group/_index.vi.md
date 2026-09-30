---
title : "Target Group"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.5.1 </b> "
---

## Tạo Target Group

**Mục tiêu:** Xác định cấu hình định tuyến để Application Load Balancer (ALB) chuyển tiếp lưu lượng đến các container Game Server đang chạy trên port `8080`.

## Các bước thực hiện

1. Truy cập **EC2 Console** → **Target Groups** → **Create target group**.

2. Cấu hình các thiết lập cơ bản:

   - **Target type**: **IP addresses** (bắt buộc đối với AWS Fargate tasks)
   - **Target group name**: `tg-game-server`
   - **Protocol**: `HTTP`
   - **Port**: `8080`
   - **IP address type**: `IPv4`
   - **VPC**: `game-server-vpc`

3. Cấu hình health check:

   - **Health check protocol**: `HTTP`
   - **Health check path**: `/health`
   - **Health check port**: Traffic port
   - **Healthy threshold**: 2
   - **Unhealthy threshold**: 3
   - **Timeout**: 5 seconds
   - **Interval**: 30 seconds

   ![Target Group Health Check Configuration](/awss-game-server-workshop/static/images/5/5.6/healcheck.png?featherlight=false&width=90pc)

4. Kiểm tra lại cấu hình và nhấn **Create target group**.

   ![Create Target Group](/awss-game-server-workshop/static/images/5/5.6/targetgr.png?featherlight=false&width=90pc)

Target Group sẽ được Application Load Balancer sử dụng để định tuyến lưu lượng đến các container Game Server đang chạy trên port `8080`.

Khi ECS Service được tích hợp với Target Group này, ECS sẽ tự động đăng ký và hủy đăng ký địa chỉ IP private của các Fargate tasks đang chạy.