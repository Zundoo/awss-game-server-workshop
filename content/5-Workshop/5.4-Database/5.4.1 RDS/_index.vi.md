---
title: "4.3.1. RDS"
weight: 431
---

# 4.3.1. Khởi tạo Cơ sở dữ liệu Amazon RDS

*   **Mục tiêu**: Thiết lập hệ thống cơ sở dữ liệu quan hệ lưu trữ thông tin tài khoản, lịch sử đấu và dữ liệu nhân vật bền vững của người chơi.
*   **Thao tác cấu hình**:
    1. Truy cập dịch vụ **Amazon RDS** > chọn **Databases** > nhấn **Create database**.
    2. Chọn phương thức **Standard create** > Engine type chọn **MySQL** (hoặc PostgreSQL tùy theo mã nguồn dự án).
    3. Mục Templates chọn **Free Tier** để tối ưu hóa chi phí thực tập.
    4. Cấu hình mục Connectivity: Chọn đúng mạng `game-server-vpc` và gán phân vùng mạng nằm hoàn toàn trong cụm **Private Subnets** để đảm bảo an toàn an ninh dữ liệu.
