---
title : "Target Group"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.6.1 </b> "
---

## Provisioning Target Group

**Objective:** Define the target routing configuration that allows the Application Load Balancer (ALB) to forward HTTP traffic to the Game Server containers running on port `8080`.

## Configuration Steps

1. Navigate to **EC2 Console** > **Target Groups** and click **Create target group**.

2. Configure the target type:

   - **Target type**: Select **IP addresses**.
   - This configuration is required when registering ECS tasks running on **AWS Fargate**.

3. Configure the target group:

   - **Target group name**: `tg-game-server`
   - **Protocol**: `HTTP`
   - **Port**: `8080`
   - **IP address type**: `IPv4`

4. For the **VPC**, select:

   `game-server-vpc`

5. Configure the health check:

   - **Health check protocol**: `HTTP`
   - **Health check path**: `/`
   - **Health check port**: `traffic port`

6. Review the configuration and click **Create target group**.

   ![IP Target Type Target Group Configuration](/images/5/5.6/5.6.1/0001.png?featherlight=false&width=90pc)

The Target Group will be used by the Application Load Balancer to route incoming HTTP traffic to the Game Server containers running on port `8080`.

When the ECS Service is integrated with the Target Group, ECS automatically registers and deregisters the IP addresses of running Fargate tasks.
