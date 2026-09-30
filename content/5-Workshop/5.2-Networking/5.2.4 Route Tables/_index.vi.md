---
title : "Route Table"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 5.2.4 </b> "
---

## Thiết lập Route Tables

Hệ thống sử dụng hai Route Table riêng biệt để kiểm soát luồng lưu lượng giữa Public Subnets và Private Subnets.

### 1. Public Route Table

Tạo một Route Table có tên `game-public-rt` dành cho các Public Subnets.

1. Từ **VPC Console**, chọn **Route tables** > nhấn **Create route table**.

2. Cấu hình các thông số sau:

   - **Name**: `game-public-rt`
   - **VPC**: `game-server-vpc`

   ![Creating Public Route Table](ight=false&width=90pc)

3. Chọn `game-public-rt` > mở tab **Routes** > nhấn **Edit routes**.

4. Thêm route sau:

   - **Destination**: `0.0.0.0/0`
   - **Target**: Internet Gateway (`game-server-igw` hoặc IGW được gắn với VPC)

   Route này cho phép các tài nguyên trong các Public Subnets được liên kết (ALB, NAT Gateway) giao tiếp với Internet thông qua Internet Gateway.

   ![Public Route Table - Routes configuration](/images/5/5.2/rtpublic2.png?featherlight=false&width=90pc)

5. Mở tab **Subnet associations** > nhấn **Edit subnet associations**.

6. Chọn các Public Subnets sau:

   - `game-public-1a` (hoặc `Public-Subnet-1A`)
   - `game-public-1b` (hoặc `Public-Subnet-1B`)

   Nhấn **Save associations**.

   ![Public Route Table - Subnet Associations](/images/5/5.2/rtpulic3.png?featherlight=false&width=90pc)
### 2. Private Route Table

Tạo một Route Table riêng có tên `game-private-rt` dành cho các Private Subnets.

1. Từ trang **Route tables**, nhấn **Create route table**.

2. Cấu hình các thông số sau:

   - **Name**: `game-private-rt`
   - **VPC**: `game-server-vpc`

   ![Creating Private Route Table](/images/5/5.2/rtprivate.png?featherlight=false&width=90pc)

3. Giữ lại route **Local** mặc định:

   - **Destination**: `10.0.0.0/16`
   - **Target**: `local`

4. Thêm route sau (quan trọng để cho phép truy cập Internet ra bên ngoài thông qua NAT):

   - **Destination**: `0.0.0.0/0`
   - **Target**: NAT Gateway (NAT Gateway được tạo trong Public Subnet)

   Route này cho phép các tài nguyên trong Private Subnets (EC2 Game Server, RDS, Redis) truy cập Internet **thông qua NAT Gateway** (để tải Docker /images, SSM Agent, cập nhật package, v.v.) trong khi vẫn không thể được truy cập trực tiếp từ Internet công cộng.

   ![Private Route Table - Routes with NAT Gateway](/images/5/5.2/rtprivate2.png?featherlight=false&width=90pc)

5. Mở tab **Subnet associations** > nhấn **Edit subnet associations**.

6. Chọn các Private Subnets sau:

   - `game-private-1a` (hoặc `Private-Subnet-1A`)
   - `game-private-1b` (hoặc `Private-Subnet-1B`)

   Nhấn **Save associations**.

   ![Private Route Table - Subnet Associations](/images/5/5.2/rtprivate3.png?featherlight=false&width=90pc)
Sau khi hoàn thành cấu hình:

- Public Subnets sử dụng `game-public-rt` → lưu lượng đi ra ngoài thông qua **Internet Gateway**.
- Private Subnets sử dụng `game-private-rt` → lưu lượng đi ra ngoài thông qua **NAT Gateway** (không có route trực tiếp đến Internet Gateway).

Thiết kế này giúp Game Server, RDS và Redis được giữ trong mạng riêng (Private Network), đồng thời vẫn cho phép các tài nguyên thực hiện những kết nối ra ngoài Internet cần thiết.