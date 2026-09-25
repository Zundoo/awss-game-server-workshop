---
title : "5.2. Networking"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.2 </b> "
---

## Cấu hình Hạ tầng mạng và Bảo mật

Phần này hướng dẫn thiết lập hệ thống mạng cô lập và an toàn trên đám mây bằng cách xây dựng **VPC**, phân chia các **Public/Private Subnets**, cấu hình **Routing** và **Security Groups** nhằm bảo vệ các tài nguyên của Game Server.

## Nội dung triển khai

1. **VPC**: Khởi tạo Virtual Private Cloud cho hệ thống.

2. **Subnets**: Phân chia Public Subnets và Private Subnets trên nhiều Availability Zones.

3. **Internet Gateway**: Cho phép các tài nguyên trong Public Subnets giao tiếp với Internet.

4. **Route Tables**: Cấu hình định tuyến giữa các Subnets và Internet Gateway.

5. **Security Groups**: Thiết lập các quy tắc Firewall để kiểm soát lưu lượng mạng giữa các tầng của hệ thống.