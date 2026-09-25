---
title: "4.1.4. Route Tables"
weight: 414
---

# 4.1.4. Thiết lập Bảng định tuyến (Route Tables)

Hệ thống cấu hình 2 bảng định tuyến riêng biệt để kiểm soát luồng đi của gói tin:

1.  **Public Route Table** (`game-public-rt`):
    *   Thêm một tuyến đường (Route): **Destination `0.0.0.0/0` \(\rightarrow\) Target: `game-server-igw`**.
    *   Gán liên kết (Explicit Subnet Associations) với 2 phân vùng mạng: `Public-Subnet-1A` và `Public-Subnet-1B`.
2.  **Private Route Table** (`game-private-rt`):
    *   Giữ nguyên cấu hình định tuyến nội bộ (`Local`), không mở đường ra Internet Gateway để đảm bảo an toàn tuyệt đối.
    *   Gán liên kết với 2 phân vùng mạng bảo mật: `Private-Subnet-1A` và `Private-Subnet-1B`.
