---
title: "4.1.1. VPC"
weight: 411
---

# 4.1.1. Khởi tạo Virtual Private Cloud (VPC)

*   **Mục tiêu**: Xây dựng một mạng diện rộng ảo cô lập hoàn toàn trên hạ tầng AWS để triển khai các tài nguyên của Game Server.
*   **Thao tác thực hiện**:
    1. Truy cập giao diện **VPC Console** > chọn **Your VPCs** > nhấn **Create VPC**.
    2. Cấu hình thông số:
        * **Name tag**: `game-server-vpc`
        * **IPv4 CIDR block**: `10.0.0.0/16` (Cung cấp tối đa 65.536 địa chỉ IP nội bộ).
    3. Nhấn **Create VPC**.
