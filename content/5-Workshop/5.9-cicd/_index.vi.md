---
title : "CI/CD"
date : "`r Sys.Date()`"
weight : 8
chapter : false
pre : " <b> 5.9 </b> "
---

# 5.9. Continuous Integration & Continuous Deployment (CI/CD) Workflow

## Quy trình Continuous Integration & Continuous Deployment (CI/CD)

This section presents the CI/CD automation pipeline for the Real-time Game Server. The workflow retrieves source code from GitHub, builds the Docker Image, pushes the image to Amazon ECR, and triggers the deployment of the updated container version on Amazon ECS using GitHub Actions.

Phần này trình bày quy trình tự động hóa CI/CD cho Real-time Game Server. Workflow thực hiện việc lấy mã nguồn từ GitHub, xây dựng Docker Image, đẩy Image lên Amazon ECR và kích hoạt quá trình triển khai phiên bản container mới trên Amazon ECS thông qua GitHub Actions.

## CI/CD Workflow

### Quy trình CI/CD

The complete automation workflow is:

Quy trình tự động hóa hoàn chỉnh:

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