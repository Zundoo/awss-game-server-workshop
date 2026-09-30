---
title : "Nhật ký Tuần 8"
date : "2026-09-14"
weight : 8
chapter : false
---

# Nhật ký học tập - Tuần 8

### Mục tiêu Tuần 8:
* Triển khai hệ thống cân bằng tải Application Load Balancer (ALB) để phân phối lưu lượng truy cập.
* Cấu hình cơ chế tự động co giãn tài nguyên Auto Scaling dựa trên nhu cầu sử dụng thực tế.
* Thực thi kịch bản kiểm thử tải bằng công cụ Artillery và phân tích dữ liệu giám sát trên Amazon CloudWatch.

### Các tác vụ thực hiện trong tuần:

| Ngày | Tác vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham chiếu |
|:---:|---|:---:|:---:|---|
| **1** | - Tìm hiểu nguyên lý định tuyến của tầng cân bằng tải công khai.<br>- Nghiên cứu cấu hình khoảng thời gian kiểm tra sức khỏe hệ thống (Health Checks) của Target Group.<br>- Thiết lập sơ đồ đón và phân phối lưu lượng đầu vào từ Internet. | 14/09/2026 | 14/09/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **2** | - Khởi tạo bộ cân bằng tải hướng ngoại Application Load Balancer công khai.<br>- Cấu hình Target Group ánh xạ chính xác cổng kết nối của container ứng dụng.<br>- Kết nối các luật xác thực trạng thái sức khỏe trực tiếp tới cụm container. | 15/09/2026 | 15/09/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **3** | - Nghiên cứu cơ chế co giãn tài nguyên linh hoạt Auto Scaling trên đám mây.<br>- So sánh các chính sách co giãn: Theo từng bước (Step Scaling) và Theo mục tiêu cố định (Target Tracking).<br>- Định nghĩa các điều kiện cảnh báo dựa trên ngưỡng tiêu hao tài nguyên phần cứng. | 16/09/2026 | 16/09/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **4** | - Gắn các chính sách tự động co giãn vào cụm dịch vụ container đang chạy.<br>- Thiết lập bộ cảnh báo (Alarms) kích hoạt khi CPU hệ thống vượt ngưỡng 70%.<br>- Chạy thử nghiệm kịch bản kích hoạt mở rộng cụm máy chủ tự động dưới áp lực giả lập. | 17/09/2026 | 17/09/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **5** | - Xây dựng tệp lệnh kịch bản kiểm thử hiệu năng hệ thống bằng công cụ Artillery.<br>- Thiết lập cấu hình truyền tải thông điệp chuỗi ký tự liên tục qua WebSocket.<br>- Định cấu hình lượng tải tập trung cao độ đạt mốc đỉnh điểm **~813 requests/phút**. | 18/09/2026 | 18/09/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **6** | - Tiến hành kích hoạt tiến trình bắn tải từ công cụ Artillery vào điểm cuối của ALB.<br>- Truy cập bộ giám sát CloudWatch để theo dõi đồ thị đo lường độ trễ `TargetResponseTime`.<br>- Kiểm tra lỗi hệ thống thời gian thực bằng cách truy vấn luồng log `game-server-stream` tập trung. | 19/09/2026 | 19/09/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **7** | - Đánh giá tổng thể độ ổn định và khả năng chịu tải của toàn bộ cấu trúc hạ tầng.<br>- Phân tích xu hướng giảm sâu của độ trễ gói tin ngay sau giai đoạn bắt tay (Cold Start).<br>- Hoàn thiện toàn bộ hồ sơ kỹ thuật, nghiệm thu hệ thống sẵn sàng vận hành thực tế. | 20/09/2026 | 20/09/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |

### Các kết quả đạt được trong Tuần 8:
* **Xây dựng cổng đón tải thông minh:** Triển khai thành công bộ cân bằng tải ALB hoạt động ổn định, phân phối mượt mà cả hai luồng kết nối HTTP truyền thống và phiên WebSocket thời gian thực.
* **Tự động hóa co giãn hạ tầng linh hoạt:** Cấu hình thành công các thuật toán giám sát phần cứng, cho phép hệ thống tự sinh thêm container để chia tải khi gặp lưu lượng đột biến và tự thu hồi khi tải giảm.
* **Xác thực hiệu năng chuẩn Production:** Vượt qua bài kiểm thử stress test nghiêm ngặt với công cụ Artillery đạt mức ~813 requests/phút; chứng minh hệ thống không bị mất mát dữ liệu và duy trì độ trễ phản hồi tiệm cận mức 0 giây lý tưởng.
