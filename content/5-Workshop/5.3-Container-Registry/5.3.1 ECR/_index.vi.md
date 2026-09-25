---
title: "4.2.1. ECR"
weight: 421
---

# 4.2.1. Khởi tạo Amazon ECR Repository

*   **Mục tiêu**: Tạo một kho lưu trữ Docker Image riêng tư bảo mật (Private Repository) trên hạ tầng AWS để quản lý các phiên bản mã nguồn của Game Server.
*   **Thao tác thực hiện**:
    1. Tìm kiếm và truy cập dịch vụ **Elastic Container Registry (ECR)** trên AWS Console.
    2. Nhấn nút **Create repository**.
    3. Cấu hình thông số:
        * **Visibility settings**: Chọn **Private**.
        * **Repository name**: Điền tên ứng dụng `game-server`.
    4. Nhấn **Create repository**.
