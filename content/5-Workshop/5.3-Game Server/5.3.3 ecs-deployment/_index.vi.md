---
title : "ECS Deployment"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 5.3.3 </b> "
---

## Tổng quan triển khai ECS

Phần này mô tả cách triển khai **Real-time Game Server** trên **Amazon Elastic Container Service (ECS)** sử dụng AWS Fargate.

Quá trình triển khai bao gồm ba thành phần chính:

1. **ECS Cluster** – Cung cấp môi trường logic để nhóm và điều phối các task của Game Server.
2. **Task Definition** – Xác định cách container được chạy (Docker image, CPU, memory, port mappings, environment variables…).
3. **ECS Service** – Duy trì số lượng task đang chạy theo mong muốn và tích hợp với Application Load Balancer.

### Kiến trúc triển khai

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