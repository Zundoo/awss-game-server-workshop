---
title : "Target Group"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.6.1 </b> "
---

## Khởi tạo Target Group

**Mục tiêu:** Xác định cấu hình định tuyến để Application Load Balancer (ALB) có thể chuyển tiếp HTTP traffic đến các Game Server container đang chạy trên port `8080`.

## Các bước cấu hình

1. Truy cập **EC2 Console** > **Target Groups** và nhấn **Create target group**.

2. Cấu hình loại Target:

   - **Target type**: Chọn **IP addresses**.
   - Cấu hình này được sử dụng khi đăng ký các ECS Task chạy trên **AWS Fargate**.

3. Cấu hình Target Group:

   - **Target group name**: `tg-game-server`
   - **Protocol**: `HTTP`
   - **Port**: `8080`
   - **IP address type**: `IPv4`

4. Tại mục **VPC**, chọn:

   `game-server-vpc`

5. Cấu hình Health Check:

   - **Health check protocol**: `HTTP`
   - **Health check path**: `/`
   - **Health check port**: `traffic port`

6. Kiểm tra lại cấu hình và nhấn **Create target group**.

   ![Cấu hình Target Group với IP Target Type](/images/5/5.6/5.6.1/0001.png?featherlight=false&width=90pc)

Target Group sẽ được Application Load Balancer sử dụng để định tuyến HTTP traffic đến các Game Server container đang chạy trên port `8080`.

Khi ECS Service được tích hợp với Target Group, ECS sẽ tự động đăng ký và hủy đăng ký địa chỉ IP của các Fargate Task đang hoạt động.