---
title : "ECS Cluster"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.5.1 </b> "
---

## Tạo Amazon ECS Cluster

**Mục tiêu:** Tạo một **Amazon Elastic Container Service (ECS) Cluster** để quản lý và điều phối các Container Task của Game Server.

## Các bước cấu hình

1. Truy cập **Amazon ECS** trên AWS Management Console.

2. Chọn **Clusters** > nhấn **Create cluster**.

3. Cấu hình các thông số:

   - **Cluster name**: `game-server-cluster`
   - **Infrastructure**: Chọn **AWS Fargate**.

   AWS Fargate cung cấp môi trường chạy container theo mô hình serverless, cho phép Game Server container hoạt động mà không cần trực tiếp quản lý các EC2 Instance bên dưới.

   ![Cấu hình ECS Cluster](/images/5/5.5/5.5.1/0001.png?featherlight=false&width=90pc)

4. Kiểm tra lại cấu hình và nhấn **Create**.

Sau khi Cluster được tạo, `game-server-cluster` sẽ sẵn sàng để triển khai các Container Task của Game Server thông qua Amazon ECS.

![ECS Cluster được khởi tạo thành công](/images/5/5.5/5.5.1/0002.png?featherlight=false&width=90pc)