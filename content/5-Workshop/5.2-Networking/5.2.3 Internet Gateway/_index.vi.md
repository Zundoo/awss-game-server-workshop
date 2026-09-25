---
title : "5.2.3. VPC"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.2.3 </b> "
---

# 5.2.3. Cấu hình Internet Gateway (IGW)

*   **Mục tiêu**: Cho phép các tài nguyên nằm trong phân vùng Public Subnet (như ALB) có khả năng giao tiếp hai chiều với mạng Internet công cộng bên ngoài.
*   **Thao tác thực hiện**:
    1. Tại menu VPC bên trái, chọn **Internet gateways** > nhấn **Create internet gateway**.
    2. Đặt tên tên tag: `game-server-igw` > nhấn **Create**.
    3. Chọn IGW vừa tạo > nhấn **Actions** > chọn **Attach to VPC** > tìm và gán vào `game-server-vpc`.
