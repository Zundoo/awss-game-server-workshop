---
title: "4.4.2. Task Definition"
weight: 442
---

# 4.4.2. Registering ECS Task Definition

*   **Objective**: Create a blueprint definition mapping the hardware allocations and Docker Image artifacts required to run the Game Server.
*   **Core Configuration Parameters**:
    1. **Task definition family**: `game-server-task`
    2. **Launch type**: `AWS Fargate`
    3. **Task size**: CPU = `0.25 vCPU`, Memory = `0.5 GB` (Minimal profile to adhere to budget constraints).
    4. **Container details**:
        * **Name**: `game-server`
        * **Image URI**: Enter your ECR registry path (e.g., `://amazonaws.com`).
        * **Port mappings**: Container Port = `8080`, Protocol = `TCP`.
    5. **Environment variables**: Pass the Redis connectivity environment keys:
        * `REDIS_HOST` = `://amazonaws.com`
        * `REDIS_PORT` = `6379`
        * `REDIS_TLS` = `true`

![Container and Environment Variables Setup in Task Definition](/images/4.4.2-task-definition.png)
