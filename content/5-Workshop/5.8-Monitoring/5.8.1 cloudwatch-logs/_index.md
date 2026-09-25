---
title: "4.7.1. CloudWatch Logs"
weight: 471
---

# 4.7.1. Configuring Log Aggregation (CloudWatch Logs)

*   **Objective**: Aggregate all system logs, active connection outputs, and real-time player chat entries from the Docker container to a centralized console.
*   **🛠️ Production Case Study - Resolving AccessDenied Failures**:
    *   *Symptom*: The CloudWatch *Log streams* interface remained empty `(0 Log streams)` even though the backend container initialized successfully.
    *   *Root Cause*: The executing IAM Role lacked specific authorization parameters required to instantiate streams and publish records to the CloudWatch endpoint.
    *   *Resolution*: Navigated to the **IAM Console**, located the system execution role, and attached the managed **`CloudWatchAgentServerPolicy`**. Concurrently, modified the Task Definition/Docker logging parameters, switching the log driver configuration to **`awslogs`** pointing to the target Log Group `/aws/ecs/game-server`.
*   **Outcomes**: All user connectivity lifecycle events and telemetry streams are tracked natively in real-time.

![CloudWatch Logs Stream View detailing player connection records](/images/4.7.1-cloudwatch-logs.png)
