---
title: "4.6.1. Auto Scaling"
weight: 461
---

# 4.6.1. Setting Up ECS Service Auto Scaling Architecture

*   **Objective**: Automatically instantiate duplicate container processing layers (Scale Out) under severe load footprints and scale back counts (Scale In) during low traffic frames to preserve project budget margins.
*   **Configuration Blueprints Parameters**:
    1. Under the ECS Service dashboard `game-server-service` > click **Update** on **Service auto scaling**.
    2. **Capacity Boundaries Limits**: Minimum tasks = `1`, Desired tasks = `1`, Maximum tasks = `3`.
    3. **Scaling policy type**: Choose **Target tracking** (Automated threshold pattern tracking specific service metrics).
    4. **ECS service metric**: Select **ECSServiceAverageCPUUtilization** (The aggregate computing processing capacity usage ratio across deployed service layers).
    5. **Target value**: Input **`70`** (Threshold definition: If average CPU capacity crosses 70%, the auto-scaler spawns new background task entities to spread traffic exhaustion).

![Target Tracking Scalability Configurations Bound at 70% CPU Threshold](/images/4.6.1-auto-scaling.png)
