---
title : "Nhật ký Tuần 4"
date : "2026-08-17"
weight : 4
chapter : false
---

# Nhật ký học tập - Tuần 4

### Mục tiêu Tuần 4:
* Tìm hiểu cơ chế kết nối cổng Internet Gateway (IGW) ra mạng ngoài.
* Học cách cấu hình định tuyến luồng dữ liệu thông qua bảng định tuyến (Route Tables).
* Triển khai hệ thống tường lửa ảo có lưu trạng thái Security Groups để bảo vệ tài nguyên.

### Các tác vụ thực hiện trong tuần:

| Ngày | Tác vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham chiếu |
|:---:|---|:---:|:---:|---|
| **1** | - Tìm hiểu cơ chế quản lý luồng dữ liệu ra vào vùng biên mạng công cộng.<br>- Nghiên cứu giao thức liên kết và gắn cổng Internet Gateway vào VPC.<br>- Lập sơ đồ hướng đi cho các gói tin mạng từ trong ra ngoài. | 17/08/2026 | 17/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **2** | - Khởi tạo một cổng Internet Gateway cụ thể trên bảng điều khiển.<br>- Tiến hành gắn kết cổng IGW vừa tạo vào mạng hệ thống VPC.<br>- Xác nhận trạng thái kích hoạt hoạt động của cổng biên mạng. | 18/08/2026 | 18/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **3** | - Tìm hiểu các thuộc tính quản trị của bảng định tuyến Route Table.<br>- So sánh tính năng của bảng định tuyến mặc định và bảng định tuyến tùy chỉnh.<br>- Học cách định nghĩa các quy tắc đích kết nối mạng (Target Destination). | 19/08/2026 | 19/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **4** | - Khởi tạo bảng định tuyến tùy chỉnh cho phân vùng mạng công cộng.<br>- Thêm luật định tuyến chuyển tiếp luồng dữ liệu `0.0.0.0/0` đi tới cổng IGW.<br>- Liên kết các Public Subnet vào bảng định tuyến hướng ngoại này. | 20/08/2026 | 20/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **5** | - Nghiên cứu nguyên lý hoạt động của tường lửa ảo trạng thái Security Groups.<br>- Phân tích cấu trúc thiết lập luật đầu vào (Inbound) và đầu ra (Outbound).<br>- So sánh phạm vi bảo vệ của Security Group với danh sách kiểm soát ACL mạng. | 21/08/2026 | 21/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **6** | - Khởi tạo các cụm tường lửa bảo mật chuyên dụng cho từng tầng thực thể.<br>- Cấu hình nhóm `alb-sg` chuyên trách mở các cổng dịch vụ công cộng 80/443.<br>- Tạo nhóm `game-server-sg` cô lập cổng ứng dụng nội bộ 8080. | 22/08/2026 | 22/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **7** | - Thực hiện kiểm thử tính liên thông và ranh giới bảo mật mạng.<br>- Xác thực các Private Subnet chặn hoàn toàn các gói tin từ Internet công cộng gửi tới.<br>- Hoàn thiện sơ đồ kết nối mạng vòng biên ban đầu. | 23/08/2026 | 23/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |

### Các kết quả đạt được trong Tuần 4:
* **Kích hoạt luồng truyền tải hướng ngoại:** Mở rộng thành công khả năng giao tiếp mạng Internet hai chiều thông qua cổng Internet Gateway biên mạng.
* **Điều phối lộ trình luồng dữ liệu:** Định hình lộ trình di chuyển của các gói tin mạng public tách biệt hoàn toàn khỏi các phân vùng chứa mã nguồn core.
* **Thiết lập tường lửa vòng biên vững chắc:** Chuẩn hóa các lớp lá chắn bảo mật phân quyền theo nguyên tắc đặc quyền tối thiểu trực tiếp tại các điểm cuối của tài nguyên.
