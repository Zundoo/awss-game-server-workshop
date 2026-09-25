---
title: "4.5.1. Target Group"
weight: 451
---

# 4.5.1. Provisioning Target Group

*   **Objective**: Define the target port routing metrics mapping to container port `8080` so the ALB knows where to proxy network frames.
*   **Configuration Steps**:
    1. From EC2 Console > under **Target Groups** > click **Create target group**.
    2. Target type: Select **IP addresses** (Mandatory constraint for integration with Amazon ECS Fargate deployment patterns).
    3. **Target group name**: `tg-game-server`
    4. **Protocol / Port**: Set to `HTTP` / Port `8080`.
    5. Ensure target is associated with `game-server-vpc`. Click **Create**.

![IP Type Target Group Parameters Configuration](/images/4.5.1-target-group.png)
