---
title: "4.4.1. ECS Cluster"
weight: 441
---

# 4.4.1. Creating Amazon ECS Cluster

*   **Objective**: Create a logical Amazon Elastic Container Service (ECS) cluster to manage and orchestrate Game Server container tasks.
*   **Configuration Steps**:
    1. Navigate to **Amazon ECS** on AWS Console > select **Clusters** > click **Create cluster**.
    2. Configure parameters:
        * **Cluster name**: `game-server-cluster`
        * **Infrastructure**: Select **AWS Fargate** (Serverless container model to optimize OS management overhead).
    3. Click **Create**.

![ECS Cluster Initialization Success](/images/4.4.1-ecs-cluster.png)
