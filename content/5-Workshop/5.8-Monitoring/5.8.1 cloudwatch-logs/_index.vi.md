---
title: "4.7.1. CloudWatch Logs"
weight: 471
---

# 4.7.1. Cấu hình Luồng thu thập Nhật ký (CloudWatch Logs)

*   **Mục tiêu**: Thu thập toàn bộ log hoạt động, log kết nối và tin nhắn chat real-time của người chơi từ Container Docker về một nơi quản lý tập trung.
*   **🛠️ Bài học kinh nghiệm sửa lỗi AccessDenied thực tế**:
    *   *Hiện tượng*: Phần mục *Log streams* trên giao diện CloudWatch bị trống `(0 Log streams)` mặc dù ứng dụng Game Server báo chạy thành công.
    *   *Nguyên nhân*: IAM Role gắn trên môi trường thực thi thiếu quyền tạo luồng và ghi dữ liệu vào dịch vụ CloudWatch.
    *   *Khắc phục*: Sinh viên truy cập dịch vụ **IAM**, tìm đến Role vận hành hệ thống và bổ sung chính sách bảo mật chuẩn **`CloudWatchAgentServerPolicy`**. Đồng thời, tại cấu hình Task Definition/Docker, kích hoạt thuộc tính log driver sang trạng thái **`awslogs`** hướng về Log Group `/aws/ecs/game-server`.
*   **Kết quả đạt được**: Toàn bộ dữ liệu nhật ký sự kiện kết nối của người chơi được lưu trữ minh bạch theo thời gian thực.

![Giao diện CloudWatch Logs Stream hiển thị rõ log kết nối của người chơi](/images/4.7.1-cloudwatch-logs.png)
