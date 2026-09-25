---
title : "Internet Gateway"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 5.2.3 </b> "
---

## Cấu hình Internet Gateway (IGW)

**Mục tiêu:** Cho phép các tài nguyên nằm trong Public Subnets, chẳng hạn như Application Load Balancer (ALB), giao tiếp với Internet thông qua Internet Gateway.

## Thao tác thực hiện

1. Tại menu VPC bên trái, chọn **Internet gateways** > nhấn **Create internet gateway**.

2. Nhập thông số sau:

   - **Name tag**: `game-server-igw`

   Nhấn **Create**.

3. Chọn Internet Gateway vừa tạo > nhấn **Actions** > chọn **Attach to VPC**.

4. Chọn `game-server-vpc` trong danh sách VPC và nhấn **Attach internet gateway**.

Internet Gateway hiện đã được gắn vào `game-server-vpc` và có thể được sử dụng bởi các tài nguyên trong Public Subnets để giao tiếp với Internet thông qua Route Table tương ứng.