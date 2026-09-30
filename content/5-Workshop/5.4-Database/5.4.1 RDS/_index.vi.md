---
title : "RDS"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.4.1 </b> "
---

## Triển khai Amazon RDS Instance

**Mục tiêu:** Triển khai hệ thống cơ sở dữ liệu quan hệ để lưu trữ an toàn thông tin người chơi, lịch sử trận đấu và dữ liệu game cần được lưu trữ lâu dài.

## Các bước thực hiện

1. Truy cập **Amazon RDS** → **Databases** → **Create database**.

2. Chọn **Standard create** và cấu hình database engine:

   - **Engine type**: `MySQL`
   - **Engine Version**: MySQL 8.0 (phiên bản mới nhất hiện có)

3. Trong mục **Templates**, chọn **Free tier** (hoặc Dev/Test) để giảm thiểu chi phí.

4. Cấu hình các thông tin database:

   - **DB instance identifier**: `game-db`
   - **Master username**: `admin`
   - **Master password**: Đặt mật khẩu mạnh (lưu trữ mật khẩu ở nơi an toàn)

5. Cấu hình **Connectivity**:

   - Chọn **Don’t connect to an EC2 compute resource**
   - **VPC**: `game-server-vpc`
   - **DB subnet group**: `game-db-subnet-group` (sử dụng Private Subnets)
   - **Public access**: **No**
   - **VPC security group**: Chọn security group có sẵn → `sg-rds`

   ![RDS Connectivity Configuration](/images/5/5.4/rdsconfic.png?featherlight=false&width=90pc)

6. Cấu hình các thiết lập bổ sung (tùy chọn):

   - Initial database name: `gamedb`
   - Tắt automated backups nếu muốn giảm chi phí trong quá trình thực hiện workshop.

7. Nhấn **Create database**.

   ![Create RDS Database](/images/5/5.4/rds2.png?featherlight=false&width=90pc)
8. Chờ cho đến khi trạng thái chuyển sang **Available** (thường mất khoảng 5–10 phút).

9. Sao chép **Endpoint** để sử dụng ở các bước sau (ví dụ):