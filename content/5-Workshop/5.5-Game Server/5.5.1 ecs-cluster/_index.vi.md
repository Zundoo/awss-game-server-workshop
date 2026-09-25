---
title: "4.4.1. ECS Cluster"
weight: 441
---

# 4.4.1. Khởi tạo Amazon ECS Cluster

*   **Mục tiêu**: Tạo một cụm logic (Cluster) bằng Amazon Elastic Container Service (ECS) để quản lý và điều phối các tác vụ Container của Game Server.
*   **Thao tác cấu hình**:
    1. Truy cập dịch vụ **Amazon ECS** trên AWS Console > chọn **Clusters** > nhấn **Create cluster**.
    2. Cấu hình thông số:
        * **Cluster name**: `game-server-cluster`
        * **Infrastructure**: Chọn **AWS Fargate** (Mô hình serverless cho container giúp tối ưu hóa việc quản trị hệ điều hành).
    3. Nhấn **Create**.

![Giao diện khởi tạo ECS Cluster thành công](/images/4.4.1-ecs-cluster.png)
