---
title : "Scaling"
date : "`r Sys.Date()`"
weight : 6
chapter : false
pre : " <b> 5.7 </b> "
---

## Dynamic Auto Scaling Architecture Configuration

This section covers the configuration of **ECS Service Auto Scaling** to dynamically adjust the number of Game Server tasks according to application workload.

The scaling architecture is designed to maintain service availability during sudden increases in player activity while reducing unnecessary compute capacity when the workload decreases.

## Implementation Overview

1. **Service Capacity**: Define the minimum, desired, and maximum number of Game Server tasks.

2. **Target Tracking Policy**: Configure `ECSServiceAverageCPUUtilization` as the scaling metric.

3. **Automatic Scale Out**: Increase the number of Game Server tasks when the service requires additional compute capacity.

4. **Automatic Scale In**: Reduce the number of running tasks when the workload decreases.

## Scaling Architecture

```text
                    Game Server Traffic
                           │
                           ▼
                 Application Load Balancer
                           │
                           ▼
                    ECS Service
                           │
                ┌──────────┴──────────┐
                │                     │
             Low Load              High Load
                │                     │
                ▼                     ▼
            Scale In              Scale Out
                │                     │
                ▼                     ▼
          Fewer Tasks             More Tasks
                │                     │
                └──────────┬──────────┘
                           ▼
                 Fargate Task Capacity
                      Min: 1
                      Max: 3