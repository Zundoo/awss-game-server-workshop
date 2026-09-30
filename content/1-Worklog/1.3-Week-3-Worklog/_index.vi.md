---
title : "Nhật ký Tuần 3"
date : "2026-08-10"
weight : 3
chapter : false
---

# Nhật ký học tập - Tuần 3

### Mục tiêu Tuần 3:
* Tìm hiểu kiến trúc thiết kế mạng đám mây Amazon Virtual Private Cloud (VPC).
* Tìm hiểu nguyên lý phân tách định tuyến giữa các phân vùng mạng (Subnets).
* Học cách phân chia dải địa chỉ IP mạng sử dụng sơ đồ định tuyến Classless Inter-Domain Routing (CIDR).

### Các tác vụ thực hiện trong tuần:

| Ngày | Tác vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham chiếu |
|:---:|---|:---:|:---:|---|
| **1** | - Nghiên cứu cơ chế vận hành của hệ thống mạng ảo hóa phần mềm.<br>- Tìm hiểu các tiêu chuẩn cô lập mạng của dịch vụ Amazon VPC.<br>- Học cách thiết kế kiến trúc mạng nội bộ biệt lập. | 10/08/2026 | 10/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **2** | - Tiến hành khởi tạo một phân vùng mạng tổng thể Amazon VPC.<br>- Cấu hình dải mạng nội bộ với block CIDR `10.0.0.0/16`.<br>- Thiết lập hệ thống thẻ tag định danh cho tài nguyên mạng. | 11/08/2026 | 11/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **3** | - Nghiên cứu kiến trúc phân chia dải mạng con Subnet.<br>- Lập sơ đồ phân phối tài nguyên trên nhiều vùng sẵn sàng (Multi-AZ) để đảm bảo High Availability.<br>- So sánh luồng đi của luồng mạng công cộng và luồng mạng nội bộ. | 12/08/2026 | 12/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **4** | - Khởi tạo các phân vùng mạng công cộng (Public Subnets).<br>- Phân bổ các dải địa chỉ IP CIDR dành riêng cho luồng mạng public.<br>- Thiết lập các cổng mạng public dự phòng trên các Availability Zone khác nhau. | 13/08/2026 | 13/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **5** | - Thiết lập cấu hình các vùng mạng cô lập (Private Subnets).<br>- Phân bổ không gian IP an toàn cho các thành phần backend và cơ sở dữ liệu.<br>- Kiểm tra ranh giới bảo mật cô lập của mạng nội bộ. | 14/08/2026 | 14/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **6** | - Tổng hợp lại sơ đồ phân bổ địa chỉ IP của toàn bộ hệ thống mạng.<br>- Rà soát các dải IP để đảm bảo không xảy ra xung đột gối chồng (overlapping).<br>- Kiểm tra lại cấu trúc ánh xạ giữa các Subnet và các vùng sẵn sàng địa lý. | 15/08/2026 | 15/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **7** | - Đánh giá lại toàn bộ tiến độ thiết lập hạ tầng mạng Core.<br>- Vẽ sơ đồ cấu trúc ranh giới mạng ảo hóa của hệ thống.<br>- Đóng gói các bản thiết kế phân chia mạng con để phục vụ triển khai về sau. | 16/08/2026 | 16/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |

### Các kết quả đạt được trong Tuần 3:
* **Xây dựng không gian mạng cô lập:** Thiết lập thành công hệ thống mạng ảo hóa VPC biệt lập, định hình không gian lưu trữ tài nguyên hệ thống an toàn bằng dải CIDR chuẩn hóa.
* **Phân chia vùng bảo mật mạng:** Tạo lập thành công các ranh giới mạng công cộng đón luồng truy cập bên ngoài kết hợp song song với mạng nội bộ chứa mã nguồn backend.
* **Tối ưu hóa kiến trúc hạ tầng:** Sắp xếp các phân vùng tài nguyên hoạt động độc lập trên cấu trúc Multi-AZ, đáp ứng tiêu chuẩn chịu lỗi của hệ thống doanh nghiệp.
