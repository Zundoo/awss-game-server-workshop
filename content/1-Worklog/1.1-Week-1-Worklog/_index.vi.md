---
title : "Nhật ký Tuần 1"
date : "2026-07-27"
weight : 1
chapter : false
---

# Nhật ký học tập - Tuần 1

### Mục tiêu Tuần 1:
* Tìm hiểu quy trình khởi tạo hạ tầng tài khoản AWS gốc.
* Thiết lập các cơ chế giám sát và quản lý chi phí AWS.
* Tìm hiểu các kiến thức cốt lõi về dịch vụ Quản lý định danh và truy cập (AWS IAM).

### Các tác vụ thực hiện trong tuần:

| Ngày | Tác vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham chiếu |
|:---:|---|:---:|:---:|---|
| **1** | - Khởi tạo tài khoản AWS cá nhân hoàn toàn mới.<br>- Thiết lập thông tin xác thực mật khẩu cho tài khoản Root.<br>- Bảo mật cổng đăng nhập hệ thống. | 27/07/2026 | 27/07/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **2** | - Tìm hiểu cơ chế xác thực đa yếu tố (MFA).<br>- Kích hoạt mã MFA ảo cho tài khoản Root.<br>- Xác thực luồng đăng nhập bảo mật hai lớp. | 28/07/2026 | 28/07/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **3** | - Nghiên cứu bảng điều khiển quản lý ngân sách AWS Budgets.<br>- Cấu hình hạn mức theo dõi chi phí ở mức 0 USD.<br>- Thiết lập email cảnh báo tự động khi chạm ngưỡng. | 29/07/2026 | 29/07/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **4** | - Tìm hiểu các tính năng hỗ trợ kỹ thuật của AWS Support.<br>- Xem xét quyền hạn của gói hỗ trợ Basic (Miễn phí).<br>- Học cách khởi tạo các phiếu yêu cầu hỗ trợ (Support Cases). | 30/07/2026 | 30/07/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **5** | - Nghiên cứu cấu trúc và nguyên lý vận hành của dịch vụ IAM.<br>- Khảo sát các khái niệm: Người dùng (Users), Nhóm (Groups), và Quyền hạn (Permissions).<br>- So sánh chính sách dựa trên thực thể danh tính và chính sách dựa trên tài nguyên. | 31/07/2026 | 31/07/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **6** | - Khởi tạo nhóm người dùng Quản trị viên (IAM Administrator User Group).<br>- Tạo tài khoản người dùng Admin riêng biệt.<br>- Áp dụng Nguyên tắc đặc quyền tối thiểu để cô lập hoàn toàn tài khoản Root. | 01/08/2026 | 01/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **7** | - Đánh giá lại các mốc bảo mật hạ tầng đã thiết lập.<br>- Thực hiện đăng nhập kiểm thử bằng tài khoản Admin vừa tạo.<br>- Sắp xếp và lưu trữ thông tin cấu hình bảo mật hệ thống. | 02/08/2026 | 02/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |

### Các kết quả đạt được trong Tuần 1:
* **Khởi tạo môi trường danh tính cốt lõi:** Thiết lập thành công môi trường thực hành đám mây AWS an toàn, được bảo vệ bằng lớp bảo mật xác thực đa yếu tố MFA cho tài khoản Root.
* **Cài đặt rào chắn chi phí:** Cấu hình thành công các kịch bản theo dõi ngân sách tự động nhằm loại bỏ rủi ro phát sinh chi phí ngoài ý muốn trong quá trình sử dụng gói Free Tier.
* **Cô lập đặc quyền quản trị tối cao:** Tạo lập cấu trúc phân quyền nhóm quản trị viên IAM rõ ràng, giúp hạn chế việc sử dụng tài khoản Root cho các hoạt động vận hành hạ tầng hàng ngày.
