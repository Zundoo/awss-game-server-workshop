---
title : "Security Groups"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 5.2.5 </b> "
---

## Firewall Rule Management (Security Groups)

Enforce the **Principle of Least Privilege** to build robust firewall perimeters for the Game Server infrastructure.

### 1. ALB Security Group

Create a Security Group named `alb-sg` for the Application Load Balancer.

* **Inbound Rules**:

  - **Type**: HTTP
  - **Port**: `80`
  - **Source**: `0.0.0.0/0`

This allows players to establish connections to the Game Server through the public Application Load Balancer.

![ALB Security Group Inbound Rules](/images/5/5.2/5.2.5/0001.png?featherlight=false&width=90pc)

### 2. Game Server Security Group

Create a Security Group named `game-server-sg` for the EC2/ECS Game Server resources.

* **Inbound Rules**:

  - **Type**: Custom TCP
  - **Port**: `8080`
  - **Source**: `alb-sg` Security Group

The source should be restricted to the **Security Group ID of the ALB (`alb-sg`)** instead of allowing traffic from `0.0.0.0/0`.

![Game Server Security Group Inbound Rules](/images/5/5.2/5.2.5/0002.png?featherlight=false&width=90pc)

This configuration prevents direct access to the Game Server from the public Internet. Only traffic forwarded through the Application Load Balancer is allowed to reach the application port `8080`.

By applying the **Principle of Least Privilege**, the ALB acts as the public entry point while the Game Server remains protected inside the private network.