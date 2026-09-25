---
title : "CloudWatch Metrics"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.8.2 </b> "
---

## Tracking Performance Indicators with CloudWatch Metrics

**Objective:** Monitor the resource utilization and traffic characteristics of the Game Server infrastructure to identify abnormal workloads, resource bottlenecks, and performance issues.

Amazon CloudWatch provides operational metrics for both the ECS Service and Application Load Balancer (ALB), allowing the infrastructure to be monitored without accessing individual containers directly.

## Core Metrics Tracked

### 1. CPUUtilization

**Namespace:** `AWS/ECS`

**Dimension:** ECS Service

`CPUUtilization` represents the average CPU utilization of the running ECS tasks.

This metric is particularly important for the configured ECS Service Auto Scaling policy, which uses CPU utilization as the target tracking metric.

### 2. MemoryUtilization

**Namespace:** `AWS/ECS`

**Dimension:** ECS Service

`MemoryUtilization` represents the percentage of memory being used by the ECS tasks.

Monitoring this metric helps identify memory pressure and potential resource constraints within the Game Server containers.

### 3. ActiveConnectionCount

**Namespace:** `AWS/ApplicationELB`

**Dimension:** Application Load Balancer

`ActiveConnectionCount` tracks the number of active connections handled by the Application Load Balancer.

This metric is useful for observing connection load, particularly for a Game Server architecture that maintains persistent client connections through the ALB.

![CloudWatch Performance Metrics Dashboard](/images/5/5.8/5.8.2/0001.png?featherlight=false&width=90pc)

## Monitoring Workflow

```text
                Game Server Infrastructure
                         │
              ┌──────────┴──────────┐
              │                     │
          ECS Service             ALB
              │                     │
              ▼                     ▼
      CPU / Memory Usage    Active Connections
              │                     │
              └──────────┬──────────┘
                         ▼
                  Amazon CloudWatch
                         │
                         ▼
                 Metrics & Dashboard