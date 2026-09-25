---
title : "Load Testing"
date : "`r Sys.Date()`"
weight : 9
chapter : false
pre : " <b> 5.10 </b> "
---

# 5.10. Infrastructure Ingress Stress & Load Testing

This section documents the technical metrics and performance analysis generated during infrastructure stress testing using **Artillery**.

The testing process evaluates the behavior of the Real-time Game Server architecture under a high-concurrency workload, with the test scenario simulating up to **1,000 concurrent WebSocket connections**.

## Testing Scope

The load testing process focuses on evaluating the following infrastructure components:

- **Application Load Balancer** — Handles incoming client connections and distributes traffic to the ECS Tasks.
- **Amazon ECS / AWS Fargate** — Runs the containerized Game Server application.
- **WebSocket Server** — Maintains persistent client connections and processes real-time messages.
- **ECS Service Auto Scaling** — Responds to increased resource utilization by adjusting the number of running Tasks.
- **Amazon CloudWatch** — Provides metrics for monitoring resource utilization, connections, and system behavior.

## Load Testing Workflow

The test traffic follows the production architecture:

```text
Artillery Load Generator
          ↓
Public ALB DNS
          ↓
Application Load Balancer
          ↓
Target Group
          ↓
ECS Fargate Tasks
          ↓
WebSocket Game Server