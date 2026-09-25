---
title: "4.5.3. Health Check"
weight: 453
---

# 4.5.3. Nghiệm thu Kiểm tra sức khỏe (Health Check)

*   **Mục tiêu**: Xác minh bộ cân bằng tải đã tìm thấy và liên kết thành công với container xử lý WebSocket bên dưới mạng Private Subnet.
*   **Kết quả cấu hình**:
    1. Truy cập Target Group `tg-game-server`, chuyển sang tab **Targets**.
    2. Sau khi ECS Service khởi chạy Task, địa chỉ IP nội bộ của container tự động đăng ký vào danh sách mục tiêu.
    3. Trạng thái cột **Health status** chuyển đổi từ *Initial* sang hiển thị màu xanh chữ **`Healthy` (1 máy chủ)**. Điều này chứng minh luồng mạng từ Internet đi qua ALB xuyên thủng tường lửa Security Group vào cổng `8080` của Container hoàn toàn thông suốt.

![Trạng thái kiểm tra sức khỏe của Target Group báo màu xanh Healthy](/images/4.5.3-health-check.png)
