---
title : "EC2 Instance"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.3.1 </b> "
---

## EC2 Instance

**Mục tiêu:** Tạo một compute instance để chạy Real-time WebSocket Game Server.

### Các bước thực hiện

1. Truy cập **EC2** → **Instances** → **Launch instances**.

2. Cấu hình các thông số sau:

   - **Name**: `game-server-01`

   - **AMI**: Amazon Linux 2023

   - **Instance type**: `t3.medium` (hoặc `t3.small`)

   - **Key pair**: Chọn hoặc tạo một key pair

   - **Network settings**:

     - **VPC**: `game-server-vpc`
     - **Subnet**: `Private-Subnet-1A` (Private Subnet)
     - **Auto-assign public IP**: **Disable**
     - **Security group**: `sg-game-server`

   - **Storage**: 20–30 GB gp3

3. Nhấn **Launch instance**.

   ![Launch EC2 Instance](/awss-game-server-workshop/static/images/5/5.2/ec2lunch.png?featherlight=false&width=90pc)

4. Gắn IAM Role với policy `AmazonSSMManagedInstanceCore` để bật quyền truy cập thông qua Session Manager.

5. Kết nối đến instance bằng **Session Manager**.

   ![EC2 Connected via Session Manager](/awss-game-server-workshop/static/images/5/5.2/ec2connect.png?featherlight=false&width=90pc)
