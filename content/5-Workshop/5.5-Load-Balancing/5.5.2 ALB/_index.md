---
title : "ALB"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.5.2 </b> "
---

## Deploying Application Load Balancer (ALB)

**Objective:** Deploy a public-facing Application Load Balancer (ALB) to receive incoming client connections and distribute traffic to the Game Server containers running in the Private Subnets.

The ALB also supports **WebSocket connections** through the HTTP listener, allowing the Game Server to maintain persistent connections with connected clients.

## Step-by-Step Implementation

1. Navigate to **EC2 Console** → **Load Balancers** → **Create load balancer**.

2. Select **Application Load Balancer** → **Create**.

3. Configure the basic settings:

   - **Load balancer name**: `alb-game-server`
   - **Scheme**: **Internet-facing**
   - **IP address type**: `IPv4`

4. Configure the **Network mapping**:

   - **VPC**: `game-server-vpc`
   - **Mappings**: Select both Availability Zones and choose the Public Subnets:
     - `Public-Subnet-1A`
     - `Public-Subnet-1B`

   ![ALB Network Mapping](/awss-game-server-workshop/static/images/5/5.6/albnetwork.png?featherlight=false&width=90pc)

5. Configure **Security groups**:

   - Select `sg-alb` (or `alb-sg`)

   The Security Group must allow inbound traffic from the public Internet on port 80 (and 443 if using HTTPS).

6. Configure the **Listeners and routing**:

   - **Protocol**: `HTTP`
   - **Port**: `80`
   - **Default action**: Forward to target group
   - **Target group**: `tg-game-server`

   ![ALB Listener Configuration](/awss-game-server-workshop/static/images/5/5.6/alblisten.png?featherlight=false&width=90pc)

7. Review the configuration and click **Create load balancer**.

   ![Create Application Load Balancer](/awss-game-server-workshop/static/images/5/5.6/albcreate.png?featherlight=false&width=90pc)

8. Wait until the ALB status becomes **Active**, then copy the **DNS name**.

After deployment, the ALB provides a public DNS endpoint that clients can use to connect to the Game Server.

### Traffic Flow

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