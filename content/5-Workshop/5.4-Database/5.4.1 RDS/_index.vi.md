---
title : "RDS"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.4.1 </b> "
---

## Khởi tạo Amazon RDS Instance

**Mục tiêu:** Triển khai hệ quản trị cơ sở dữ liệu quan hệ để lưu trữ an toàn thông tin người chơi, lịch sử trận đấu và dữ liệu vật phẩm cần được duy trì lâu dài.

## Cấu hình kiến trúc

1. Truy cập **Amazon RDS** > chọn **Databases** > nhấn **Create database**.

2. Chọn **Standard create** và cấu hình Database Engine:
   - **Engine type**: `MySQL`
   - Có thể chọn PostgreSQL nếu phù hợp với technology stack của ứng dụng.

3. Trong mục **Templates**, chọn **Free tier** để giảm chi phí trong phạm vi Workshop.

4. Cấu hình kết nối Database:
   - **VPC**: Chọn `game-server-vpc`.
   - Cấu hình DB Subnet Group sử dụng các **Private Subnets**.
   - Không đặt Database trực tiếp trong Public Subnet.

   ![Cấu hình kết nối RDS](/images/5/5.4/5.4.1/0001.png?featherlight=false&width=90pc)

5. Cấu hình các thông số của Database Instance theo yêu cầu của Workshop và kiểm tra lại toàn bộ cấu hình.

6. Nhấn **Create database**.

Sau khi được khởi tạo, RDS Instance sẽ hoạt động bên trong VPC và không cho phép truy cập trực tiếp từ Internet. Game Server có thể kết nối đến Database thông qua mạng Private bằng các quy tắc Security Group phù hợp.