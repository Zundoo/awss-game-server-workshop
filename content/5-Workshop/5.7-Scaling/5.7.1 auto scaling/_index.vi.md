
### Vietnamese — `5.7.1 Auto Scaling`

```markdown
---
title : "Auto Scaling"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.7.1 </b> "
---

## Thiết lập ECS Service Auto Scaling

**Mục tiêu:** Cấu hình ECS Service Auto Scaling để tự động điều chỉnh số lượng Game Server Task đang chạy dựa trên mức độ tải của ứng dụng.

Cơ chế Scaling cho phép Service **Scale Out** bằng cách khởi chạy thêm Task khi mức sử dụng CPU tăng và **Scale In** bằng cách giảm số lượng Task khi tải hệ thống giảm.

## Các bước cấu hình

1. Truy cập **Amazon ECS** > **Clusters** > `game-server-cluster`.

2. Chọn ECS Service:

   `game-server-service`

3. Mở phần **Service auto scaling** và chọn **Update** hoặc cấu hình Scaling Policy.

4. Cấu hình giới hạn số lượng Task:

   - **Minimum number of tasks**: `1`
   - **Desired number of tasks**: `1`
   - **Maximum number of tasks**: `3`

5. Cấu hình Scaling Policy:

   - **Policy type**: **Target tracking**
   - **ECS service metric**: `ECSServiceAverageCPUUtilization`
   - **Target value**: `70%`

   ![Cấu hình Target Tracking với ngưỡng CPU 70%](/images/5/5.7/5.7.1/0001.png?featherlight=false&width=90pc)

6. Lưu cấu hình.

## Cơ chế hoạt động

ECS Service sẽ tự động điều chỉnh số lượng Task đang chạy dựa trên mức sử dụng CPU trung bình của Service.

```text
                  ECS Service
                       │
                       ▼
                CPU trung bình
                       │
             ┌─────────┴─────────┐
             │                   │
           Tải cao             Tải thấp
             │                   │
             ▼                   ▼
         Scale Out            Scale In
             │                   │
             ▼                   ▼
       Thêm Fargate Task    Giảm Fargate Task
             │                   │
             └─────────┬─────────┘
                       ▼
              Số lượng Task mong muốn
                 Min: 1 / Max: 3