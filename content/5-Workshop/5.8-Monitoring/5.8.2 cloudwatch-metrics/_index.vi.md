---
title : "CloudWatch Metrics"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.8.2 </b> "
---

## Theo dõi các chỉ số hiệu năng với CloudWatch Metrics

**Mục tiêu:** Theo dõi mức sử dụng tài nguyên và đặc điểm traffic của Game Server nhằm phát hiện workload bất thường, bottleneck tài nguyên và các vấn đề về hiệu năng.

Amazon CloudWatch cung cấp các metric cho cả ECS Service và Application Load Balancer (ALB), cho phép giám sát hạ tầng mà không cần truy cập trực tiếp vào từng container.

## Các Metric chính

### 1. CPUUtilization

**Namespace:** `AWS/ECS`

**Dimension:** ECS Service

`CPUUtilization` biểu thị mức sử dụng CPU trung bình của các ECS Task đang hoạt động.

Metric này đặc biệt quan trọng đối với cấu hình ECS Service Auto Scaling vì CPU utilization được sử dụng làm metric cho Target Tracking Policy.

### 2. MemoryUtilization

**Namespace:** `AWS/ECS`

**Dimension:** ECS Service

`MemoryUtilization` biểu thị phần trăm bộ nhớ đang được sử dụng bởi các ECS Task.

Theo dõi metric này giúp phát hiện tình trạng thiếu bộ nhớ và các giới hạn tài nguyên bên trong Game Server container.

### 3. ActiveConnectionCount

**Namespace:** `AWS/ApplicationELB`

**Dimension:** Application Load Balancer

`ActiveConnectionCount` theo dõi số lượng connection đang hoạt động được Application Load Balancer xử lý.

Metric này hữu ích để quan sát mức tải kết nối, đặc biệt đối với kiến trúc Game Server sử dụng các kết nối persistent thông qua ALB.

![CloudWatch Performance Metrics Dashboard](/images/5/5.8/5.8.2/0001.png?featherlight=false&width=90pc)

## Quy trình giám sát

```text
                Game Server Infrastructure
                         │
              ┌──────────┴──────────┐
              │                     │
          ECS Service             ALB
              │                     │
              ▼                     ▼
       CPU / Memory Usage    Active Connections
              │                     │
              └──────────┬──────────┘
                         ▼
                  Amazon CloudWatch
                         │
                         ▼
                 Metrics & Dashboard