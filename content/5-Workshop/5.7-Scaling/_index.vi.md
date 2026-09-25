---
title : "Scaling"
date : "`r Sys.Date()`"
weight : 6
chapter : false
pre : " <b> 5.7 </b> "
---

## Cấu hình kiến trúc Dynamic Auto Scaling

Phần này trình bày cấu hình **ECS Service Auto Scaling** nhằm tự động điều chỉnh số lượng Game Server Task dựa trên workload của ứng dụng.

Kiến trúc Scaling được thiết kế để duy trì khả năng phục vụ khi số lượng người chơi tăng đột biến, đồng thời giảm tài nguyên tính toán không cần thiết khi workload giảm.

## Tổng quan triển khai

1. **Service Capacity**: Xác định số lượng Game Server Task tối thiểu, mong muốn và tối đa.

2. **Target Tracking Policy**: Sử dụng `ECSServiceAverageCPUUtilization` làm metric theo dõi Scaling.

3. **Automatic Scale Out**: Tăng số lượng Game Server Task khi Service cần thêm năng lực xử lý.

4. **Automatic Scale In**: Giảm số lượng Task đang chạy khi workload giảm.

## Kiến trúc Scaling

```text
                    Game Server Traffic
                           │
                           ▼
                 Application Load Balancer
                           │
                           ▼
                    ECS Service
                           │
                ┌──────────┴──────────┐
                │                     │
             Tải thấp              Tải cao
                │                     │
                ▼                     ▼
            Scale In              Scale Out
                │                     │
                ▼                     ▼
        Giảm số lượng Task       Tăng số lượng Task
                │                     │
                └──────────┬──────────┘
                           ▼
                 Fargate Task Capacity
                      Min: 1
                      Max: 3