---
title : "Database"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 5.4 </b> "
---

## Cấu hình Database và Cache Tier

Phần này hướng dẫn triển khai lớp **Database** và **Cache** cần thiết cho **Real-time Game Server**.

**Amazon RDS** được sử dụng để lưu trữ dữ liệu Game Server cần được duy trì lâu dài như thông tin người chơi, lịch sử trận đấu và trạng thái vật phẩm. Trong khi đó, **Amazon ElastiCache for Redis** cung cấp lớp dữ liệu trong bộ nhớ với độ trễ thấp, phục vụ Session State và các dữ liệu Game cần truy cập thường xuyên trong thời gian thực.

## Tổng quan triển khai

1. **Amazon RDS**: Triển khai cơ sở dữ liệu quan hệ trong mạng Private để lưu trữ dữ liệu lâu dài của Game Server.

2. **Amazon ElastiCache for Redis**: Triển khai Redis Cluster để cung cấp khả năng truy cập nhanh đến Session và trạng thái Game theo thời gian thực.

3. **Network Security**: Giới hạn quyền truy cập đến Database và Cache chỉ cho các tài nguyên Game Server được cấp phép thông qua Security Groups và kết nối mạng Private.

## Kiến trúc Database

Database và Cache Tier được cô lập khỏi truy cập trực tiếp từ Internet:

```text
              Game Server
                   │
          ┌────────┴────────┐
          │                 │
          ▼                 ▼
      Amazon RDS      ElastiCache Redis
    Dữ liệu lâu dài    Session / Cache
          │                 │
          └──── Mạng Private ────┘