---
title: "4.5.2. ALB"
weight: 452
---

# 4.5.2. Deploying Application Load Balancer (ALB)

*   **Objective**: Set up a public-facing load balancer responsible for receiving entry connections and managing automated protocol upgrades from stateless HTTP to persistent real-time WebSockets.
*   **Configuration Steps**:
    1. From EC2 Console > under **Load Balancers** > click **Create load balancer** > choose **Application Load Balancer**.
    2. **Load balancer name**: `alb-game-server`
    3. **Scheme**: Select **Internet-facing** (Accept public traffic streams).
    4. **Network mapping**: Select `game-server-vpc` and explicitly check the **Public Subnets** configurations (`Public-Subnet-1A`, `Public-Subnet-1B`).
    5. **Security groups**: Bind the `alb-sg` firewall group.
    6. **Listeners and routing**: Inbound `HTTP:80` > under *Default action* choose Forward to `tg-game-server`. Click **Create**.

![Public Subnets Allocation for Internet-Facing Application Load Balancer](/images/4.5.2-alb.png)
