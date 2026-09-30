---
title : "Internet Gateway"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 5.2.3 </b> "
---

## Cấu hình Internet Gateway (IGW)

**Mục tiêu:** Cho phép các tài nguyên nằm trong Public Subnets (chẳng hạn như Application Load Balancer và NAT Gateway) giao tiếp với Internet công cộng.

## Các bước thực hiện

1. Từ menu **VPC** ở phía bên trái, chọn **Internet gateways** > nhấn **Create internet gateway**.

2. Nhập thông tin sau:

   - **Name tag**: `game-server-igw`

   Nhấn **Create internet gateway**.

   ![Create Internet Gateway](images/5/5.2/igw1.png?featherlight=false&width=90pc)

3. Chọn Internet Gateway vừa tạo (`game-server-igw`) > nhấn **Actions** > chọn **Attach to VPC**.

4. Chọn `game-server-vpc` từ danh sách VPC và nhấn **Attach internet gateway**.

5. Kiểm tra trạng thái:

   - Internet Gateway phải hiển thị **State: Attached**
   - Internet Gateway được liên kết với `game-server-vpc`

   ![Internet Gateway Attached Successfully](images/5/5.2/igw2.png?featherlight=false&width=90pc)

Internet Gateway hiện đã được gắn với `game-server-vpc` và có thể được sử dụng bởi các tài nguyên trong Public Subnets để giao tiếp với Internet thông qua Public Route Table (`0.0.0.0/0` → Internet Gateway).