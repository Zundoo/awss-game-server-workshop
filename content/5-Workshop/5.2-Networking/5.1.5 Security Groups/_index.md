---
title: "4.1.5. Security Groups"
weight: 415
---

# 4.1.5. Firewall Rule Management (Security Groups)

Enforce the Principle of Least Privilege to build robust firewall perimeters:

*   **ALB Security Group** (`alb-sg`):
    *   **Inbound Rules**: Open public `HTTP Port 80` to all sources (`0.0.0.0/0`) to accept player connections.
*   **EC2/ECS Game Server Security Group** (`game-server-sg`):
    *   **Inbound Rules**: Open internal application port `Custom TCP Port 8080`. Crucial configuration restriction: **Set source strictly to the security group ID of the ALB (`alb-sg`)**. This completely blocks all direct network scanning or unauthorized ingress from the public internet.
