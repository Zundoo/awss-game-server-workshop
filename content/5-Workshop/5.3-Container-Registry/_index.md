---
title : "Container"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.3 </b> "
---

## Containerization & Container Image Management

This section covers the process of containerizing the **Node.js WebSocket Game Server**, creating a secure private container repository on **Amazon Elastic Container Registry (ECR)**, and publishing the built Docker images for use by the Game Server infrastructure.

## Implementation Overview

1. **ECR Repository**: Create a private Amazon ECR repository to securely store and manage Game Server container images.

2. **Docker Image**: Create a lightweight Docker image for the Node.js WebSocket Game Server using a Dockerfile.

3. **Push Image**: Authenticate Docker with Amazon ECR, build the image, tag it with the ECR repository URI, and push it to the repository.

## Containerization Workflow

The containerization process follows this workflow:

```text
Node.js Game Server
        │
        ▼
    Dockerfile
        │
        ▼
  Docker Build
        │
        ▼
   Docker Image
        │
        ▼
   Amazon ECR
        │
        ▼
     Amazon ECS