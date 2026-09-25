---
title : "CI/CD"
date : "`r Sys.Date()`"
weight : 8
chapter : false
pre : " <b> 5.9 </b> "
---

# 5.9. Continuous Integration & Continuous Deployment (CI/CD) Workflow

This section outlines the CI/CD automation pipeline for the Real-time Game Server. The workflow retrieves source code from GitHub, builds the Docker Image, pushes the image to the private Amazon ECR repository, and updates the container deployment on Amazon ECS using GitHub Actions.

## CI/CD Workflow

The complete automation workflow is:

```text
GitHub Repository
       ↓
GitHub Actions
       ↓
Checkout Source Code
       ↓
Configure AWS Credentials
       ↓
Build Docker Image
       ↓
Push Image to Amazon ECR
       ↓
Update ECS Service
       ↓
ECS Rolling Update
       ↓
ALB Health Check
       ↓
New Game Server Version