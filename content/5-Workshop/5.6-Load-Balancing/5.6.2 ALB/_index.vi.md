---
title: "4.5.2. ALB"
weight: 452
---

# 4.5.2. Tạo bộ Application Load Balancer (ALB)

*   **Mục tiêu**: Thiết lập bộ cân bằng tải công khai chịu trách nhiệm nhận kết nối và tự động chuyển đổi nâng cấp giao thức mạng từ HTTP sang WebSocket bền vững.
*   **Thao tác cấu hình**:
    1. Tại EC2 Console > mục **Load Balancers** > nhấn **Create load balancer** > loại **Application Load Balancer**.
    2. **Load balancer name**: `alb-game-server`
    3. **Scheme**: Chọn **Internet-facing** (Đón traffic công cộng).
    4. **Network mapping**: Chọn `game-server-vpc` và tích chọn các **Public Subnets** (`Public-Subnet-1A`, `Public-Subnet-1B`).
    5. **Security groups**: Gán nhóm bảo mật `alb-sg`.
    6. **Listeners and routing**: Cổng `HTTP:80` > mục *Default action* chọn Forward to `tg-game-server`. Nhấn **Create**.

![Cấu hình phân vùng mạng Public Subnets cho bộ cân bằng tải ALB](/images/4.5.2-alb.png)
