---
title : "Route Tables"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 5.2.4 </b> "
---

## Thiết lập Route Tables

Hệ thống sử dụng hai Route Table riêng biệt để kiểm soát lưu lượng mạng giữa Public Subnets và Private Subnets.

### 1. Public Route Table

Tạo một Route Table có tên `game-public-rt` dành cho các Public Subnets.

1. Tại VPC Console, chọn **Route tables** > nhấn **Create route table**.

2. Cấu hình các thông số:

   - **Name**: `game-public-rt`
   - **VPC**: `game-server-vpc`

   ![Tạo Public Route Table](/images/5/5.2/5.2.4/0001.png?featherlight=false&width=90pc)

3. Chọn `game-public-rt` > mở tab **Routes** > nhấn **Edit routes**.

4. Thêm route sau:

   - **Destination**: `0.0.0.0/0`
   - **Target**: `game-server-igw`

   Route này cho phép các tài nguyên trong Public Subnets được liên kết với Route Table giao tiếp với Internet thông qua Internet Gateway.

   ![Cấu hình Public Route Table](/images/5/5.2/5.2.4/0002.png?featherlight=false&width=90pc)

5. Mở tab **Subnet associations** > nhấn **Edit subnet associations**.

6. Chọn hai Public Subnets:

   - `Public-Subnet-1A`
   - `Public-Subnet-1B`

   Nhấn **Save associations**.

   ![Liên kết Public Subnets](/images/5/5.2/5.2.4/0003.png?featherlight=false&width=90pc)

### 2. Private Route Table

Tạo một Route Table riêng có tên `game-private-rt` dành cho các Private Subnets.

1. Tại trang **Route tables**, nhấn **Create route table**.

2. Cấu hình các thông số:

   - **Name**: `game-private-rt`
   - **VPC**: `game-server-vpc`

3. Giữ nguyên route mặc định **Local**:

   - **Destination**: `10.0.0.0/16`
   - **Target**: `local`

   Không cấu hình route đến Internet Gateway cho Route Table này. Điều này ngăn các tài nguyên trong Private Subnets truy cập trực tiếp ra Internet.

4. Mở tab **Subnet associations** > nhấn **Edit subnet associations**.

5. Chọn hai Private Subnets:

   - `Private-Subnet-1A`
   - `Private-Subnet-1B`

   Nhấn **Save associations**.

   ![Private Route Table và Subnet Associations](/images/5/5.2/5.2.4/0004.png?featherlight=false&width=90pc)

Sau khi hoàn tất cấu hình, Public Subnets sử dụng `game-public-rt` để truy cập Internet thông qua Internet Gateway, trong khi Private Subnets sử dụng `game-private-rt` và không có route trực tiếp đến Internet Gateway.