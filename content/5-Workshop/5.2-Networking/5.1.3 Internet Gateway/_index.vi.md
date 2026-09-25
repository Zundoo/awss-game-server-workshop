---
title: "4.1.3. Internet Gateway"
weight: 413
---

# 4.1.3. Cấu hình Internet Gateway (IGW)

*   **Mục tiêu**: Cho phép các tài nguyên nằm trong phân vùng Public Subnet (như ALB) có khả năng giao tiếp hai chiều với mạng Internet công cộng bên ngoài.
*   **Thao tác thực hiện**:
    1. Tại menu VPC bên trái, chọn **Internet gateways** > nhấn **Create internet gateway**.
    2. Đặt tên tên tag: `game-server-igw` > nhấn **Create**.
    3. Chọn IGW vừa tạo > nhấn **Actions** > chọn **Attach to VPC** > tìm và gán vào `game-server-vpc`.
