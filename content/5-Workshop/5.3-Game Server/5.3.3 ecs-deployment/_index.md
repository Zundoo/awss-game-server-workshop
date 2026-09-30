---
title : "ECS Deployment"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 5.3.3 </b> "
---

## ECS Deployment Overview

This section describes the deployment of the Real-time Game Server on **Amazon Elastic Container Service (ECS)** using AWS Fargate.

The deployment consists of three main components:

1. **ECS Cluster** – Provides the logical grouping and orchestration environment for the Game Server tasks.
2. **Task Definition** – Defines how the container should run (Docker image, CPU, memory, port mappings, environment variables…).
3. **ECS Service** – Maintains the desired number of running tasks and integrates with the Application Load Balancer.

### Deployment Architecture

```text
Amazon ECR (Docker Image)
          │
          ▼
   ECS Task Definition
          │
          ▼
      ECS Service
          │
          ▼
      ECS Cluster
          │
          ▼
   AWS Fargate Tasks
          │
          ▼
  Game Server (Port 8080)