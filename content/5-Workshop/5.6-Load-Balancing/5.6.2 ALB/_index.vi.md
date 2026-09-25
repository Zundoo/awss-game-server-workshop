
### Vietnamese — `5.6.2 ALB`

```markdown
---
title : "ALB"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.6.2 </b> "
---

## Triển khai Application Load Balancer (ALB)

**Mục tiêu:** Triển khai Application Load Balancer (ALB) hướng Internet để tiếp nhận các kết nối từ Client và phân phối traffic đến các Game Server container đang chạy trong Private Subnets.

ALB hỗ trợ **WebSocket connection** thông qua HTTP/HTTPS Listener, cho phép Game Server duy trì các kết nối liên tục với Client.

## Các bước cấu hình

1. Truy cập **EC2 Console** > **Load Balancers** và nhấn **Create load balancer**.

2. Chọn **Application Load Balancer**.

3. Cấu hình các thông số cơ bản:

   - **Load balancer name**: `alb-game-server`
   - **Scheme**: **Internet-facing**
   - **IP address type**: `IPv4`

4. Cấu hình **Network mapping**:

   - **VPC**: Chọn `game-server-vpc`.
   - **Availability Zones và Subnets**:
     - `Public-Subnet-1A`
     - `Public-Subnet-1B`

   ![Phân bổ Public Subnets cho Internet-facing Application Load Balancer](/images/5/5.6/5.6.2/0001.png?featherlight=false&width=90pc)

5. Cấu hình **Security groups**:

   - Chọn `alb-sg`.

   Security Group cần cho phép traffic từ Internet đi vào trên port được sử dụng bởi Listener.

6. Cấu hình **Listener và Routing**:

   - **Protocol**: `HTTP`
   - **Port**: `80`
   - **Default action**: **Forward to**
   - **Target group**: `tg-game-server`

7. Kiểm tra lại cấu hình và nhấn **Create load balancer**.

Sau khi triển khai thành công, ALB sẽ cung cấp một Public DNS endpoint để Client có thể sử dụng nhằm kết nối đến Game Server.

Luồng traffic:

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