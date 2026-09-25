---
title: "4.4.3. ECS Service"
weight: 443
---

# 4.4.3. Khởi chạy ứng dụng với ECS Service

*   **Mục tiêu**: Vận hành và duy trì số lượng Task ổn định trong phân vùng Private Subnet.
*   **Thao tác cấu hình**:
    1. Trong cụm `game-server-cluster`, tại tab **Services** chọn **Create**.
    2. Chọn Task Definition `game-server-task` phiên bản mới nhất.
    3. **Desired tasks**: Điền `1` (Số lượng container chạy ban đầu).
    4. **Networking**: 
        * Chọn `game-server-vpc`.
        * Chọn các **Private Subnets** (`Private-Subnet-1A`, `Private-Subnet-1B`).
        * Security Group: Chọn `game-server-sg`.

![Trạng thái dịch vụ ECS Service chạy ổn định độc lập](/images/4.4.3-ecs-service.png)
