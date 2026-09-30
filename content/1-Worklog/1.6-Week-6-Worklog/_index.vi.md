---
title : "Nhật ký Tuần 6"
date : "2026-08-31"
weight : 6
chapter : false
---

# Nhật ký học tập - Tuần 6

### Mục tiêu Tuần 6:
* Tìm hiểu quy trình biên dịch mã nguồn thành hình ảnh ứng dụng Docker Image.
* Tìm hiểu dịch vụ điều phối và quản lý container Amazon Elastic Container Service (ECS).
* Học cách cấu hình và quản lý vòng đời của các phân luồng container ứng dụng (Tasks).

### Các tác vụ thực hiện trong tuần:

| Ngày | Tác vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham chiếu |
|:---:|---|:---:|:---:|---|
| **1** | - Nghiên cứu quy trình ảo hóa ứng dụng ở cấp độ hệ điều hành.<br>- Tìm hiểu cấu trúc thiết lập các tham số xây dựng trong tệp `Dockerfile`.<br>- Phân tích cơ chế tối ưu hóa kích thước ảnh thông qua kỹ thuật lưu bộ nhớ đệm phân tầng (layer caching). | 31/08/2026 | 31/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **2** | - Tiến hành viết tệp cấu hình `Dockerfile` đa tầng (multi-stage) cho ứng dụng game server.<br>- Biên dịch mã nguồn máy chủ trò chơi thành các gói Docker Image dung lượng tối giản.<br>- Kiểm tra trạng thái khởi chạy của container trong môi trường cục bộ để xác minh. | 01/09/2026 | 01/09/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **3** | - Tìm hiểu toàn diện kiến trúc sinh thái của dịch vụ Amazon ECS.<br>- Phân tích các mô hình triển khai: Không máy chủ AWS Fargate và quản lý máy chủ EC2.<br>- Nghiên cứu các mô hình thiết kế bảng điều khiển điều phối container. | 02/09/2026 | 02/09/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **4** | - Triển khai một trung tâm điều phối container Amazon ECS Cluster hoàn chỉnh.<br>- Cấu hình cấu trúc phân bổ tài nguyên Fargate cấp độ micro để tối ưu chi phí.<br>- Thiết lập các quy tắc quản lý nguồn lực tính toán cho container đám mây. | 03/09/2026 | 03/09/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **5** | - Học cách thiết lập cú pháp cấu hình trong bản đặc tả Task Definition.<br>- Định nghĩa hạn mức dung lượng RAM và sức mạnh CPU cho từng container.<br>- Thiết lập cấu hình các biến môi trường kết nối hệ thống cho container. | 04/09/2026 | 04/09/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **6** | - Khởi chạy một dịch vụ quản lý container Amazon ECS Service chạy môi trường production.<br>- Thiết lập luật duy trì số lượng container mục tiêu hoạt động liên tục.<br>- Liên kết các nhóm container đang chạy vào hệ thống bảo mật mạng nội bộ. | 05/09/2026 | 05/09/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **7** | - Tiến hành kiểm tra và xác thực quy trình phân phối ứng dụng container hóa.<br>- Khảo sát nhật ký hệ thống (Logs) trong quá trình khởi động dịch vụ container.<br>- Chuẩn hóa các biểu mẫu tệp lệnh phục vụ tự động hóa build ảnh. | 06/09/2026 | 06/09/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |

### Các kết quả đạt được trong Tuần 6:
* **Chuẩn hóa môi trường chạy ứng dụng:** Đóng gói thành công mã nguồn ứng dụng thô thành các gói Docker Image độc lập, nhỏ gọn và dễ dàng di chuyển.
* **Làm chủ bộ máy điều phối Container:** Thiết kế và vận hành thành công kiến trúc container tự động thông qua công cụ điều khiển đám mây Amazon ECS.
* **Tách biệt tầng xử lý và phần cứng máy chủ:** Cô lập thành công môi trường ứng dụng chạy độc lập, giảm thiểu sự phụ thuộc vào cấu hình của hệ thống máy chủ vật lý bên dưới.
