---
title : "5.2.5. VPC"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.2.5 </b> "
---
# 5.2.5. Cấu hình Luật tường lửa (Security Groups)

Áp dụng nguyên tắc đặc quyền tối thiểu (Least Privilege) để thiết lập lá chắn bảo mật:

*   **ALB Security Group** (`alb-sg`):
    *   **Inbound Rules**: Mở cổng mạng công khai `HTTP Port 80` cho mọi nguồn (`0.0.0.0/0`) để đón người chơi kết nối vào.
*   **EC2/ECS Game Server Security Group** (`game-server-sg`):
    *   **Inbound Rules**: Mở cổng ứng dụng nội bộ `Custom TCP Port 8080`. Cấu hình nguồn đi vào nghiêm ngặt: **Chỉ cho phép duy nhất từ nhóm bảo mật mã định danh của ALB (`alb-sg`)**. Chặn đứng hoàn toàn mọi kết nối dò quét cổng trực tiếp từ Internet.
