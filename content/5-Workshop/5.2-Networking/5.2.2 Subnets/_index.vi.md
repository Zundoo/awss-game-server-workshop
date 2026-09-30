---
title : "Subnets"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.2.2 </b> "
---

## Phân chia Subnet

Để tối ưu bảo mật bằng cách sử dụng **3-Tier Architecture**, mạng được phân chia thành các Public Subnets và Private Subnets, được triển khai trên ít nhất 2 Availability Zones (AZs).

### Public Subnets

**Mục đích:** Chứa các tài nguyên cần cho phép truy cập trực tiếp từ Internet (Application Load Balancer, NAT Gateway).

- `Public-Subnet-1A` (CIDR: `10.0.1.0/24`) trong AZ `ap-southeast-1a`
- `Public-Subnet-1B` (CIDR: `10.0.2.0/24`) trong AZ `ap-southeast-1b`

### Private Subnets

**Mục đích:** Chứa các tài nguyên nội bộ không nên được truy cập trực tiếp từ Internet (EC2 Game Server, RDS, ElastiCache Redis).

- `Private-Subnet-1A` (CIDR: `10.0.11.0/24`) trong AZ `ap-southeast-1a`
- `Private-Subnet-1B` (CIDR: `10.0.12.0/24`) trong AZ `ap-southeast-1b`

---

## Các bước thực hiện

1. Từ **VPC Console**, chọn **Subnets** > nhấn **Create subnet**.

2. Cấu hình các thông số sau cho Public Subnet đầu tiên:

   - **VPC ID**: `game-server-vpc`
   - **Subnet name**: `Public-Subnet-1A`
   - **Availability Zone**: `ap-southeast-1a`
   - **IPv4 CIDR block**: `10.0.1.0/24`

   Nhấn **Add new subnet** để tiếp tục tạo các subnet còn lại trong cùng wizard.

   ![Create Public Subnet 1A](images/5/5.2/subnet1.png?featherlight=false&width=90pc)

3. Tạo Public Subnet thứ hai:

   - **Subnet name**: `Public-Subnet-1B`
   - **Availability Zone**: `ap-southeast-1b`
   - **IPv4 CIDR block**: `10.0.2.0/24`

4. Tạo Private Subnet đầu tiên:

   - **Subnet name**: `Private-Subnet-1A`
   - **Availability Zone**: `ap-southeast-1a`
   - **IPv4 CIDR block**: `10.0.11.0/24`

5. Tạo Private Subnet thứ hai:

   - **Subnet name**: `Private-Subnet-1B`
   - **Availability Zone**: `ap-southeast-1b`
   - **IPv4 CIDR block**: `10.0.12.0/24`

   Nhấn **Create subnet**.

   ![Create All Subnets](images/5/5.2/subnet2.png?featherlight=false&width=90pc)

6. (Tùy chọn nhưng được khuyến nghị) Bật **Auto-assign public IPv4 address** cho các Public Subnets:

   - Chọn từng Public Subnet → **Actions** → **Edit subnet settings**
   - Chọn **Enable auto-assign public IPv4 address** → Save

   ![Enable Auto-assign Public IP](images/5/5.2/subnet3.png?featherlight=false&width=90pc)
Sau khi hoàn thành, bạn sẽ có 4 subnet như được tổng hợp dưới đây:

| Tên Subnet           | CIDR            | Availability Zone   | Loại    |
|----------------------|-----------------|---------------------|---------|
| Public-Subnet-1A     | 10.0.1.0/24     | ap-southeast-1a     | Public  |
| Public-Subnet-1B     | 10.0.2.0/24     | ap-southeast-1b     | Public  |
| Private-Subnet-1A    | 10.0.11.0/24    | ap-southeast-1a     | Private |
| Private-Subnet-1B    | 10.0.12.0/24    | ap-southeast-1b     | Private |

![Subnets Overview](images/5/5.2/subnet.png?featherlight=false&width=90pc)