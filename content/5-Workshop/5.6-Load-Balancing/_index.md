---
title : "Load Balancing"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 5.6 </b> "
---

## Application Load Balancer Architecture Configuration

This section covers the configuration of the **Application Load Balancer (ALB)** architecture used to expose the Real-time Game Server to external clients.

The configuration includes creating a **Target Group** for the ECS Fargate tasks, deploying an **Internet-facing Application Load Balancer**, and validating the health status of the registered Game Server targets.

## Implementation Overview

1. **Target Group**: Configure the target routing to the Game Server containers running on port `8080`.

2. **Application Load Balancer**: Deploy an Internet-facing ALB inside the Public Subnets to receive incoming client connections.

3. **Health Check**: Verify that the ALB can successfully reach and monitor the health of the Game Server tasks.

## Load Balancing Architecture

```text
                         Internet
                            │
                            │ HTTP :80
                            ▼
                ┌───────────────────────┐
                │   Application Load    │
                │      Balancer         │
                │    alb-game-server    │
                └───────────┬───────────┘
                            │
                            │ Forward
                            ▼
                ┌───────────────────────┐
                │    tg-game-server     │
                │     Target Group      │
                └───────────┬───────────┘
                            │
                            │ HTTP :8080
                            ▼
                ┌───────────────────────┐
                │    ECS Fargate Task   │
                │      Game Server      │
                └───────────────────────┘