---
title : "Redis"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.4.2 </b> "
---

## Cấu hình Cụm bộ nhớ đệm ElastiCache Redis

**Mục tiêu:** Triển khai cụm **Amazon ElastiCache for Redis** để xử lý dữ liệu Session và hỗ trợ đồng bộ trạng thái phòng Game theo thời gian thực giữa nhiều Game Server.

Redis được triển khai trong **Private Subnets** của `game-server-vpc` và chỉ cho phép các Game Server được cấp quyền kết nối đến Redis.

## Cấu hình ElastiCache Redis

1. Truy cập **Amazon ElastiCache** trên AWS Management Console.

2. Chọn **Redis caches** > nhấn **Create Redis cache**.

3. Cấu hình các thông số của Redis theo yêu cầu của Workshop.

4. Đảm bảo Redis được triển khai trong mạng Private và sử dụng Security Group cho phép Game Server kết nối đến Redis.

   - **Redis Port**: `6379`
   - **VPC**: `game-server-vpc`
   - **Subnet**: Private Subnets

   ![ElastiCache Redis Configuration](/images/5/5.4/5.4.2/0001.png?featherlight=false&width=90pc)

---

## 🛠️ Nhật ký Sửa lỗi: Khắc phục sự cố kết nối Redis do TLS

### Hiện tượng lỗi

Khi thực hiện kiểm tra kết nối Redis từ máy chủ EC2 bằng lệnh CLI thông thường:

```bash
redis6-cli -h <REDIS_ENDPOINT> -p 6379