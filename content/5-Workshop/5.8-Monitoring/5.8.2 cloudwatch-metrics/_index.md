---
title: "4.7.2. CloudWatch Metrics"
weight: 472
---

# 4.7.2. Tracking Performance Indicators (CloudWatch Metrics)

*   **Objective**: Manage and evaluate server resource utilization baselines to proactively identify network performance choke points or compute spikes.
*   **Core Metrics Tracked**:
    1.  **CPUUtilization (ECS Service)**: Aggregate CPU execution footprint across active game containers.
    2.  **MemoryUtilization**: Memory consumption metrics across the operational container layer.
    3.  **ActiveConnectionCount (Application ALB)**: Total active persistent WebSocket sessions mapped directly into the infrastructure topology.

![Performance Metrics Chart showcasing stable computing resources](/images/4.7.2-cloudwatch-metrics.png)
