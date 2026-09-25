---
title : "Auto Scaling"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.7.1 </b> "
---

## Setting Up ECS Service Auto Scaling

**Objective:** Configure ECS Service Auto Scaling to automatically adjust the number of running Game Server tasks according to application workload.

The scaling policy allows the service to **scale out** by launching additional tasks when CPU utilization increases and **scale in** by reducing the number of tasks when the workload decreases.

## Configuration Steps

1. Navigate to **Amazon ECS** > **Clusters** > `game-server-cluster`.

2. Select the ECS Service:

   `game-server-service`

3. Open the **Service auto scaling** configuration and select **Update** or configure the scaling policy.

4. Configure the service capacity:

   - **Minimum number of tasks**: `1`
   - **Desired number of tasks**: `1`
   - **Maximum number of tasks**: `3`

5. Configure the scaling policy:

   - **Policy type**: **Target tracking**
   - **ECS service metric**: `ECSServiceAverageCPUUtilization`
   - **Target value**: `70%`

   ![Target Tracking Scaling Configuration at 70% CPU Threshold](/images/5/5.7/5.7.1/0001.png?featherlight=false&width=90pc)

6. Save the configuration.

## Scaling Behavior

The ECS Service automatically adjusts the number of running tasks based on the average CPU utilization of the service.

```text
                  ECS Service
                       │
                       ▼
             Average CPU Utilization
                       │
             ┌─────────┴─────────┐
             │                   │
          High Load           Low Load
             │                   │
             ▼                   ▼
          Scale Out            Scale In
             │                   │
             ▼                   ▼
      Add Fargate Tasks    Reduce Fargate Tasks
             │                   │
             └─────────┬─────────┘
                       ▼
              Desired Task Count
                Min: 1 / Max: 3