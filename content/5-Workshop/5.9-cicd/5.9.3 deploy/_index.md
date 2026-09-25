---
title: "4.8.3. Deploy"
weight: 483
---

# 4.8.3. Executing Zero-Downtime Deployment Upgrades

*   **Objective**: Roll out new ECR image builds down to the live ECS Service layer, replacing old server contexts without triggering disconnect spikes for active players.
*   **Execution Strategy**: The CI/CD script raises an explicit force deployment flag via `aws ecs update-service`.
*   **Outcomes**: The ECS scheduler provisions a **Rolling Update** strategy: Starts the new container \(\rightarrow\) waits for the ALB targets checks to turn *Healthy* \(\rightarrow\) then terminates legacy container footprints, ensuring zero user disconnection.

![CI/CD Execution Log Workflow showcasing passing green status on GitHub](/images/4.8.3-deploy.png)
