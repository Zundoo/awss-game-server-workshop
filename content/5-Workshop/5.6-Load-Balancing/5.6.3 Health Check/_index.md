---
title : "Health Check"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 5.6.3 </b> "
---

## Validating Target Health Checks

**Objective:** Verify that the Application Load Balancer (ALB) can successfully reach the Game Server containers running inside the Private Subnets and that the registered ECS targets are healthy.

## Verification Steps

1. Navigate to **EC2 Console** > **Target Groups**.

2. Select the target group:

   `tg-game-server`

3. Open the **Targets** tab.

4. Once the ECS Service successfully launches the Game Server task, ECS automatically registers the task's private IP address with the Target Group.

5. Monitor the **Health status** of the registered target.

6. The target should transition from **Initial** to:

   **Healthy**

   ![Target Group Routing Target In-Service Healthy Verification Status](/images/5/5.6/5.6.3/0001.png?featherlight=false&width=90pc)

A **Healthy** status confirms that the ALB can successfully perform the configured health check against the Game Server container on port `8080`.

The traffic path is therefore validated as:

```text
Internet
    │
    ▼
Internet-facing ALB
    │
    ▼
tg-game-server
    │
    │ HTTP :8080
    ▼
ECS Fargate Task
    │
    ▼
Game Server