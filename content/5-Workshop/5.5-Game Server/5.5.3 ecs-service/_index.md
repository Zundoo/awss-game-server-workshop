---
title: "4.4.3. ECS Service"
weight: 443
---

# 4.4.3. Deploying Runtime via ECS Service

*   **Objective**: Deploy, monitor, and maintain a stable count of tasks instances inside the isolated Private Subnet perimeters.
*   **Configuration Steps**:
    1. Inside `game-server-cluster`, under the **Services** tab, click **Create**.
    2. Choose the latest revision of Task Definition `game-server-task`.
    3. **Desired tasks**: Set to `1` (Initial boot container instance count).
    4. **Networking**: 
        * Select `game-server-vpc`.
        * Force subnets to **Private Subnets** (`Private-Subnet-1A`, `Private-Subnet-1B`).
        * Security Group: Choose `game-server-sg`.

![ECS Service Running Tasks Instance Status](/images/4.4.3-ecs-service.png)
