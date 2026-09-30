---
title : "Redis"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.4.2 </b> "
---

## Cấu hình ElastiCache Redis

**Mục tiêu:** Triển khai một cluster **Amazon ElastiCache for Redis** để xử lý dữ liệu session và hỗ trợ đồng bộ trạng thái phòng game theo thời gian thực giữa nhiều Game Server.

Redis được triển khai trong **Private Subnets** của `game-server-vpc` và chỉ các tài nguyên Game Server được cấp quyền mới có thể thiết lập kết nối đến Redis.

## Các bước thực hiện

1. Truy cập **Amazon ElastiCache** → **Redis OSS caches** → **Create Redis OSS cache**.

2. Cấu hình các thông số sau:

   - **Deployment option**: Design your own cache
   - **Creation method**: Cluster cache
   - **Cluster mode**: Disabled
   - **Name**: `game-redis`
   - **Engine version**: 7.x (hoặc phiên bản mới nhất hiện có)
   - **Node type**: `cache.t3.micro` (hoặc `cache.t4g.micro`)
   - **Number of replicas**: 0

3. Cấu hình networking:

   - **Subnet group**: `game-redis-subnet-group` (Private Subnets)
   - **VPC**: `game-server-vpc`
   - **Security groups**: Chọn `sg-redis`
   - **Encryption in transit**: Disabled (để thuận tiện cho việc kiểm thử trong workshop)

   ![ElastiCache Redis Configuration](images/5/5.4/redis.png?featherlight=false&width=90pc)

4. Nhấn **Create**.

5. Chờ cho đến khi trạng thái chuyển sang **Available** (thường mất khoảng 5–8 phút).

6. Sao chép **Primary endpoint**: