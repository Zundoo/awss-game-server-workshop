---
title : "Target Group"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.5.1 </b> "
---

## Provisioning Target Group

**Objective:** Define the target routing configuration that allows the Application Load Balancer (ALB) to forward traffic to the Game Server containers running on port `8080`.

## Step-by-Step Implementation

1. Navigate to **EC2 Console** → **Target Groups** → **Create target group**.

2. Configure the basic settings:

   - **Target type**: **IP addresses** (required for AWS Fargate tasks)
   - **Target group name**: `tg-game-server`
   - **Protocol**: `HTTP`
   - **Port**: `8080`
   - **IP address type**: `IPv4`
   - **VPC**: `game-server-vpc`

3. Configure the health check:

   - **Health check protocol**: `HTTP`
   - **Health check path**: `/health`
   - **Health check port**: Traffic port
   - **Healthy threshold**: 2
   - **Unhealthy threshold**: 3
   - **Timeout**: 5 seconds
   - **Interval**: 30 seconds

   ![Target Group Health Check Configuration](/awss-game-server-workshop//images/5/5.6/healcheck.png?featherlight=false&width=90pc)

4. Review the configuration and click **Create target group**.

   ![Create Target Group](/images/5/5.6/targetgr.png?featherlight=false&width=90pc)
The Target Group will be used by the Application Load Balancer to route incoming traffic to the Game Server containers running on port `8080`.

When the ECS Service is integrated with this Target Group, ECS automatically registers and deregisters the private IP addresses of the running Fargate tasks.