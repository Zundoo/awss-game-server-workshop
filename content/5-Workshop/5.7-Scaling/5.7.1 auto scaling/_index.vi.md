---
title: "4.6.1. Auto Scaling"
weight: 461
---

# 4.6.1. Thiết lập Cấu hình Amazon ECS Service Auto Scaling

*   **Mục tiêu**: Tự động nhân bản số lượng Container (Scale Out) khi chịu tải nặng và tự động hủy bỏ giảm số lượng máy (Scale In) khi thấp điểm để tối ưu hóa ngân sách.
*   **Thông số thiết lập cấu hình**:
    1. Tại giao diện ECS Service `game-server-service` > mục **Service auto scaling** chọn **Update**.
    2. **Quy mô co giãn giới hạn**: Minimum tasks = `1`, Desired tasks = `1`, Maximum tasks = `3`.
    3. **Scaling policy type**: Chọn **Target tracking** (Tự động bám đuổi theo chỉ số tài nguyên chỉ định).
    4. **ECS service metric**: Chọn **ECSServiceAverageCPUUtilization** (Tỷ lệ sử dụng tài nguyên vi xử lý trung bình của dịch vụ).
    5. **Target value**: Điền **`70`** (Ngưỡng kích hoạt: Nếu trung bình CPU vượt ngưỡng 70%, hệ thống tự động tạo thêm Task mới để san sẻ chia lửa gánh tải).

![Thiết lập chính sách tự động co giãn bám đuổi CPU ngưỡng 70%](/images/4.6.1-auto-scaling.png)
