---
title : "WebSocket Test"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.10.2 </b> "
---

# 5.10.2. Persistent WebSocket High-Concurrency Stress Test

This test evaluates the behavior of the Real-time Game Server under a high-concurrency WebSocket workload.

The **Artillery** load-testing tool is executed from a local console and targets the public **Application Load Balancer DNS hostname**.

The test simulates a sudden user spike by creating **1,000 virtual users within approximately 1 second** and generating **46,500 WebSocket messages** during the test.

## Test Configuration

The load test uses the following configuration:

| Parameter | Value |
|---|---:|
| Virtual Users | 1,000 |
| WebSocket Messages | 46,500 |
| WebSocket Send Rate | 1,629 messages/sec |
| Total Test Duration | 35 seconds |

The test traffic follows the production request path:

```text
Artillery
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