---
title : "Security Groups"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 5.2.5 </b> "
---

## Quản lý Quy tắc Tường lửa (Security Groups)

Áp dụng **Principle of Least Privilege (Nguyên tắc đặc quyền tối thiểu)** để xây dựng lớp tường lửa bảo vệ cho hạ tầng Game Server.

### 1. Security Group cho ALB

Tạo một Security Group có tên `alb-sg` dành cho Application Load Balancer.

* **Inbound Rules**:

  - **Type**: HTTP
  - **Port**: `80`
  - **Source**: `0.0.0.0/0`

Cấu hình này cho phép người chơi thiết lập kết nối đến Game Server thông qua Application Load Balancer công khai.

![ALB Security Group Inbound Rules](/images/5/5.2/5.2.5/0001.png?featherlight=false&width=90pc)

### 2. Security Group cho Game Server

Tạo một Security Group có tên `game-server-sg` dành cho các tài nguyên EC2/ECS Game Server.

* **Inbound Rules**:

  - **Type**: Custom TCP
  - **Port**: `8080`
  - **Source**: Security Group `alb-sg`

Source phải được giới hạn ở **Security Group ID của ALB (`alb-sg`)** thay vì cho phép truy cập từ `0.0.0.0/0`.

![Game Server Security Group Inbound Rules](/images/5/5.2/5.2.5/0002.png?featherlight=false&width=90pc)

Cấu hình này ngăn chặn việc truy cập trực tiếp từ Internet đến Game Server. Chỉ lưu lượng được chuyển tiếp thông qua Application Load Balancer mới được phép truy cập vào port ứng dụng `8080`.

Bằng cách áp dụng **Principle of Least Privilege**, ALB đóng vai trò là điểm truy cập công khai duy nhất, trong khi Game Server được bảo vệ bên trong mạng Private.