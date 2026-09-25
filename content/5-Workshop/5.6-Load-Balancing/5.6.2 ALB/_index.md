---
title : "ALB"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.6.2 </b> "
---

## Deploying Application Load Balancer (ALB)

**Objective:** Deploy a public-facing Application Load Balancer (ALB) to receive incoming client connections and distribute traffic to the Game Server containers running in the Private Subnets.

The ALB also supports **WebSocket connections** through the HTTP/HTTPS listener, allowing the Game Server to maintain persistent connections with connected clients.

## Configuration Steps

1. Navigate to **EC2 Console** > **Load Balancers** and click **Create load balancer**.

2. Select **Application Load Balancer**.

3. Configure the basic settings:

   - **Load balancer name**: `alb-game-server`
   - **Scheme**: **Internet-facing**
   - **IP address type**: `IPv4`

4. Configure the **Network mapping**:

   - **VPC**: Select `game-server-vpc`.
   - **Availability Zones and Subnets**:
     - `Public-Subnet-1A`
     - `Public-Subnet-1B`

   ![Public Subnets Allocation for Internet-Facing Application Load Balancer](/images/5/5.6/5.6.2/0001.png?featherlight=false&width=90pc)

5. Configure **Security groups**:

   - Select `alb-sg`.

   The Security Group should allow inbound traffic from the public Internet on the listener port.

6. Configure the **Listener and routing**:

   - **Protocol**: `HTTP`
   - **Port**: `80`
   - **Default action**: **Forward to**
   - **Target group**: `tg-game-server`

7. Review the configuration and click **Create load balancer**.

After deployment, the ALB provides a public DNS endpoint that can be used by clients to establish connections to the Game Server.

The traffic flow is:

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