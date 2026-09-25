
### Vietnamese — `5.5 Game Server`

```markdown
---
title : "Game Server"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 5.5 </b> "
---

## Triển khai Game Server trên Amazon ECS

Phần này hướng dẫn triển khai **Real-time Game Server** sử dụng Amazon Elastic Container Service (ECS).

Quy trình triển khai bao gồm khởi tạo ECS Cluster, định nghĩa cấu hình runtime thông qua ECS Task Definition và khởi chạy Game Server bằng ECS Service bên trong môi trường Private Subnet được bảo vệ.

## Tổng quan triển khai

1. **ECS Cluster**: Tạo Amazon ECS Cluster để quản lý và điều phối các Container Task của Game Server.

2. **Task Definition**: Định nghĩa tài nguyên tính toán, Docker Image, Container Port và các biến môi trường cần thiết cho Game Server.

3. **ECS Service**: Khởi chạy và duy trì các Game Server Task bên trong Private Subnets sử dụng AWS Fargate.

## Quy trình triển khai Game Server

```text
              Amazon ECR
                   │
                   │ Docker Image
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
          AWS Fargate Task
                   │
                   ▼
          Game Server :8080