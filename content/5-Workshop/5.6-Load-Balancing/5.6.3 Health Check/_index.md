---
title: "4.5.3. Health Check"
weight: 453
---

# 4.5.3. Validating In-Service Target Health Checks

*   **Objective**: Confirm the public load balancer successfully registers and establishes end-to-end socket probes with the isolated WebSocket containers inside the Private Subnets.
*   **Verification Outcomes**:
    1. Access Target Group `tg-game-server`, switch to the **Targets** tab.
    2. Once the ECS Service executes the application tasks, the container's private IP automatically binds into the routing list.
    3. The **Health status** tracking column shifts from *Initial* to a bright green **`Healthy` (1 instance)** text state. This validates that the external internet traffic entering the ALB safely navigates through firewall boundaries down to container port `8080`.

![Target Group Routing Target In-Service Healthy Verification Status](/images/4.5.3-health-check.png)
