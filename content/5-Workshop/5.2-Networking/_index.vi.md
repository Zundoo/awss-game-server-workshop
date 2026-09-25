---
title : "Networking"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.2 </b> "
---

## Cấu hình Hạ tầng Mạng và Bảo mật

Phần này hướng dẫn thiết lập hệ thống mạng cô lập và an toàn trên đám mây bằng cách xây dựng **VPC**, cấu hình **Public/Private Subnets**, thiết lập **Routing** và triển khai **Security Groups** để bảo vệ các tài nguyên của Game Server.

## Tổng quan triển khai

1. **VPC**: Khởi tạo Virtual Private Cloud cho hạ tầng Game Server.

2. **Subnets**: Phân chia mạng thành Public Subnets và Private Subnets trên nhiều Availability Zones.

3. **Internet Gateway**: Cho phép các tài nguyên trong Public Subnets giao tiếp với Internet.

4. **Route Tables**: Cấu hình định tuyến giữa các Subnets và Internet Gateway.

5. **Security Groups**: Cấu hình các quy tắc tường lửa để kiểm soát lưu lượng mạng giữa các tầng khác nhau của hệ thống.