---
title : "Health Check"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 5.6.3 </b> "
---

## Kiểm tra trạng thái Health Check của Target

**Mục tiêu:** Xác minh Application Load Balancer (ALB) có thể kết nối thành công đến các Game Server container đang chạy bên trong Private Subnets và các ECS Target đã đăng ký đang ở trạng thái hoạt động bình thường.

## Các bước kiểm tra

1. Truy cập **EC2 Console** > **Target Groups**.

2. Chọn Target Group:

   `tg-game-server`

3. Mở tab **Targets**.

4. Sau khi ECS Service khởi chạy thành công Game Server Task, ECS sẽ tự động đăng ký địa chỉ IP Private của Task vào Target Group.

5. Theo dõi cột **Health status** của Target đã đăng ký.

6. Target sẽ chuyển từ trạng thái **Initial** sang:

   **Healthy**

   ![Trạng thái Healthy của Target trong Target Group](/images/5/5.6/5.6.3/0001.png?featherlight=false&width=90pc)

Trạng thái **Healthy** xác nhận rằng ALB có thể thực hiện Health Check thành công đối với Game Server container thông qua port `8080`.

Luồng traffic được xác nhận:

```text
Internet
    │
    ▼
Internet-facing ALB
    │
    ▼
tg-game-server
    │
    │ HTTP :8080
    ▼
ECS Fargate Task
    │
    ▼
Game Server