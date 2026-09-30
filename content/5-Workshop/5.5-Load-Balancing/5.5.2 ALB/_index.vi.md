---
title : "ALB"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.5.2 </b> "
---

## Triển khai Application Load Balancer (ALB)

**Mục tiêu:** Triển khai một Application Load Balancer (ALB) hướng Internet để tiếp nhận các kết nối từ client và phân phối lưu lượng đến các container Game Server đang chạy trong Private Subnets.

ALB cũng hỗ trợ **WebSocket connections** thông qua HTTP listener, cho phép Game Server duy trì các kết nối liên tục với các client đã kết nối.

## Các bước thực hiện

1. Truy cập **EC2 Console** → **Load Balancers** → **Create load balancer**.

2. Chọn **Application Load Balancer** → **Create**.

3. Cấu hình các thiết lập cơ bản:

   - **Load balancer name**: `alb-game-server`
   - **Scheme**: **Internet-facing**
   - **IP address type**: `IPv4`

4. Cấu hình **Network mapping**:

   - **VPC**: `game-server-vpc`
   - **Mappings**: Chọn cả hai Availability Zones và các Public Subnets:
     - `Public-Subnet-1A`
     - `Public-Subnet-1B`

   ![ALB Network Mapping](/awss-game-server-workshop/static/images/5/5.6/albnetwork.png?featherlight=false&width=90pc)

5. Cấu hình **Security groups**:

   - Chọn `sg-alb` (hoặc `alb-sg`)

   Security Group phải cho phép lưu lượng inbound từ Internet công cộng trên port 80 (và port 443 nếu sử dụng HTTPS).

6. Cấu hình **Listeners and routing**:

   - **Protocol**: `HTTP`
   - **Port**: `80`
   - **Default action**: Forward to target group
   - **Target group**: `tg-game-server`

   ![ALB Listener Configuration](/awss-game-server-workshop/static/images/5/5.6/alblisten.png?featherlight=false&width=90pc)

7. Kiểm tra lại cấu hình và nhấn **Create load balancer**.

   ![Create Application Load Balancer](/awss-game-server-workshop/static/images/5/5.6/albcreate.png?featherlight=false&width=90pc)

8. Chờ cho đến khi trạng thái của ALB chuyển sang **Active**, sau đó sao chép **DNS name**.

Sau khi triển khai, ALB sẽ cung cấp một public DNS endpoint mà client có thể sử dụng để kết nối đến Game Server.

### Luồng lưu lượng

```text
Internet
    │
    │ HTTP :80
    ▼
Internet-facing ALB
    │
    │ Forward
    ▼
tg-game-server
    │
    │ HTTP :8080
    ▼
ECS Fargate Task
    │
    ▼
Game Server