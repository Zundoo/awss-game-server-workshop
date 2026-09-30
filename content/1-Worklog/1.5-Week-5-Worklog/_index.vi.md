---
title : "Nhật ký Tuần 5"
date : "2026-08-24"
weight : 5
chapter : false
---

# Nhật ký học tập - Tuần 5

### Mục tiêu Tuần 5:
* Triển khai hệ thống cơ sở dữ liệu quan hệ Amazon Relational Database Service (RDS).
* Thiết lập cụm cơ sở dữ liệu bộ nhớ đệm phân tán Amazon ElastiCache Redis.
* Cấu hình cô lập bảo mật tuyệt đối cho tầng dữ liệu lưu trữ nội bộ.

### Các tác vụ thực hiện trong tuần:

| Ngày | Tác vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham chiếu |
|:---:|---|:---:|:---:|---|
| **1** | - Tìm hiểu các kiến trúc thiết kế tầng dữ liệu đám mây.<br>- Nghiên cứu các lựa chọn nền tảng công cụ cơ sở dữ liệu trên Amazon RDS.<br>- Học cách cấu hình nhóm mạng con cơ sở dữ liệu cô lập (DB Subnet Groups). | 24/08/2026 | 24/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **2** | - Khởi tạo một thực thể cơ sở dữ liệu RDS MySQL chuyên dụng.<br>- Đặt thực thể hoạt động hoàn toàn bên trong phân vùng Private Subnet nội bộ.<br>- Thiết lập các luật tường lửa ảo chuyên biệt cho cổng kết nối của database. | 25/08/2026 | 25/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **3** | - Nghiên cứu yêu cầu về độ trễ micro giây của tầng dữ liệu đệm.<br>- Tìm hiểu cơ chế quản lý bộ nhớ của dịch vụ ElastiCache Redis.<br>- Khảo sát mô hình kiến trúc tin nhắn Pub/Sub thời gian thực phục vụ hệ thống WebSocket. | 26/08/2026 | 26/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **4** | - Tiến hành khởi tạo một nút cơ sở dữ liệu bộ nhớ đệm ElastiCache Redis.<br>- Cấu hình ánh xạ cổng kết nối dữ liệu đệm trên port tiêu chuẩn 6379.<br>- Ràng buộc quyền truy cập dữ liệu đệm chỉ dành riêng cho tầng ứng dụng. | 27/08/2026 | 27/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **5** | - Thiết lập mô hình bắt tay kết nối bảo mật giữa các tầng kiến trúc.<br>- Cấu hình cụm `rds-sg` chặn đứng hoàn toàn mọi lệnh dò quét IP công cộng.<br>- Giới hạn đường dẫn kết nối đầu vào chỉ chấp nhận nguồn từ máy chủ game. | 28/08/2026 | 28/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **6** | - Chạy các vòng lặp lệnh kiểm thử khả năng liên thông dữ liệu nội bộ.<br>- Xác thực các tiến trình truyền tải thông tin diễn ra mượt mà trong mạng riêng.<br>- Giám sát các chỉ số trạng thái sức khỏe của công cụ lưu trữ database. | 29/08/2026 | 29/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **7** | - Đánh giá lại toàn bộ trạng thái hoạt động của các tầng lưu trữ dữ liệu.<br>- Ghi nhận thông tin điểm cuối truy cập (Endpoints) của database tổng.<br>- Sao lưu các bảng cấu hình cài đặt mạng nền tảng để lưu trữ hồ sơ. | 30/08/2026 | 30/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |

### Các kết quả đạt được trong Tuần 5:
* **Triển khai thành công lõi cơ sở dữ liệu bảo mật:** Tạo lập thành công các thực thể cơ sở dữ liệu quan hệ sẵn sàng vận hành, nằm ẩn bên trong các vùng mạng nội bộ của doanh nghiệp.
* **Tối ưu hóa tốc độ truy xuất dữ liệu:** Khởi chạy thành công bộ máy phản hồi dữ liệu đệm tốc độ cao, đáp ứng điều kiện xử lý thông điệp liên tục của game.
* **Triệt tiêu hoàn toàn nguy cơ tấn công mạng:** Cô lập thành công toàn bộ tài sản dữ liệu nhạy cảm phía sau các lớp rào chắn Security Group vững chắc.
