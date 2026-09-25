---
title : "Container"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.3 </b> "
---

## Containerization và Quản lý Container Image

Phần này hướng dẫn quá trình đóng gói **Node.js WebSocket Game Server** thành Docker Container, tạo Private Repository trên **Amazon Elastic Container Registry (ECR)** và đưa Docker Image lên ECR để sử dụng trong hạ tầng Game Server.

## Tổng quan triển khai

1. **ECR Repository**: Tạo Private ECR Repository để lưu trữ và quản lý an toàn các Container Image của Game Server.

2. **Docker Image**: Xây dựng Docker Image nhẹ cho Node.js WebSocket Game Server bằng Dockerfile.

3. **Push Image**: Xác thực Docker với Amazon ECR, build Image, gắn ECR Repository URI và push Image lên Repository.

## Quy trình Containerization

Quy trình đóng gói và lưu trữ Container Image được thực hiện theo luồng:

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