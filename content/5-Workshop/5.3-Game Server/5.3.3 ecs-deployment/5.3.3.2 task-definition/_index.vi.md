---
title : "Task Definition"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.5.2 </b> "
---

## Đăng ký ECS Task Definition

**Mục tiêu:** Tạo một Task Definition mô tả các tài nguyên tính toán, Docker Image, cấu hình container và các biến môi trường cần thiết để chạy Game Server trên Amazon ECS.

## Các thông số cấu hình chính

1. **Task definition family**: `game-server-task`

2. **Launch type**: `AWS Fargate`

3. **Task size**:
   - **CPU**: `0.25 vCPU`
   - **Memory**: `0.5 GB`

   Cấu hình tài nguyên tối thiểu này phù hợp với môi trường Workshop và giúp giảm chi phí triển khai.

4. **Container details**:

   - **Name**: `game-server`
   - **Image URI**:

     ```text
     <AWS_ACCOUNT_ID>.dkr.ecr.ap-southeast-1.amazonaws.com/game-server:latest
     ```

   - **Port mappings**:
     - **Container port**: `8080`
     - **Protocol**: `TCP`

5. **Environment variables**:

   Cấu hình các biến môi trường để Game Server kết nối đến Redis:

   | Variable | Value |
   |---|---|
   | `REDIS_HOST` | `<REDIS_ENDPOINT>` |
   | `REDIS_PORT` | `6379` |
   | `REDIS_TLS` | `true` |

   ![Cấu hình Container và Environment Variables trong Task Definition](/images/5/5.5/5.5.2/0001.png?featherlight=false&width=90pc)

6. Kiểm tra lại cấu hình Task Definition và nhấn **Create**.

Sau khi Task Definition được đăng ký, revision của `game-server-task` có thể được sử dụng bởi ECS Service để khởi chạy các Game Server container trên AWS Fargate.