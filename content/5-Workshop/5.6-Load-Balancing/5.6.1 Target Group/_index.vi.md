---
title: "4.5.1. Target Group"
weight: 451
---

# 4.5.1. Khởi tạo Nhóm mục tiêu (Target Group)

*   **Mục tiêu**: Định nghĩa điểm đích định tuyến cổng `8080` của Container để ALB biết nơi chuyển tiếp gói tin dữ liệu game.
*   **Thao tác cấu hình**:
    1. Tại EC2 Console > mục **Target Groups** > nhấn **Create target group**.
    2. Target type: Chọn **IP addresses** (Bắt buộc khi tích hợp làm bộ cân bằng tải cho Amazon ECS Fargate).
    3. **Target group name**: `tg-game-server`
    4. **Protocol / Port**: Chọn `HTTP` / Cổng `8080`.
    5. Chọn đúng `game-server-vpc`. Nhấn **Create**.

![Cấu hình thông số định danh Target Group loại IP](/images/4.5.1-target-group.png)
