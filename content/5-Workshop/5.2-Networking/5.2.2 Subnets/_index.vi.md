---
title : "Subnets"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.2.2 </b> "
---

## Phân chia Phân vùng mạng (Subnets)

Để tối ưu hóa bảo mật theo mô hình 3 lớp (3-Tier Architecture), hệ thống được chia thành các phân vùng Public và Private trải rộng trên ít nhất 2 Availability Zones (AZs):

### Public Subnets

**Tiếp nhận traffic Internet:**

- `Public-Subnet-1A` (CIDR: `10.0.1.0/24`) tại AZ `ap-southeast-1a`.

- `Public-Subnet-1B` (CIDR: `10.0.2.0/24`) tại AZ `ap-southeast-1b`.

### Private Subnets

**Cô lập máy chủ và Cơ sở dữ liệu:**

- `Private-Subnet-1A` (CIDR: `10.0.11.0/24`) tại AZ `ap-southeast-1a`.

- `Private-Subnet-1B` (CIDR: `10.0.12.0/24`) tại AZ `ap-southeast-1b`.