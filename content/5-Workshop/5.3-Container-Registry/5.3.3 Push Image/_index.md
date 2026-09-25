---
title : "Push Image"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 5.3.3 </b> "
---

## Pushing Docker Image to Amazon ECR

After creating the ECR repository and configuring the Dockerfile, build the Game Server Docker image and push it to the private Amazon ECR repository.

## Step-by-Step Implementation

Open a terminal in the root directory of the Game Server project and execute the following commands.

### 1. Authenticate Docker with Amazon ECR

Authenticate the Docker CLI against the private ECR registry:

```bash
aws ecr get-login-password --region ap-southeast-1 | docker login --username AWS --password-stdin <AWS_ACCOUNT_ID>.dkr.ecr.ap-southeast-1.amazonaws.com