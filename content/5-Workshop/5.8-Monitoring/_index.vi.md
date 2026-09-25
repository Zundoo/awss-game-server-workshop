
### Vietnamese — `5.8 Monitoring`

```markdown
---
title : "Monitoring"
date : "`r Sys.Date()`"
weight : 7
chapter : false
pre : " <b> 5.8 </b> "
---

## Giám sát tập trung với Amazon CloudWatch

Phần này trình bày việc triển khai **Amazon CloudWatch** để giám sát tập trung hạ tầng Real-time Game Server.

CloudWatch được sử dụng để thu thập log từ các container và theo dõi các metric của hạ tầng, cung cấp khả năng quan sát hành vi của ứng dụng, mức sử dụng tài nguyên và hoạt động của các Client connection.

## Tổng quan triển khai

1. **CloudWatch Logs**: Tập trung các log được tạo bởi Game Server container để phục vụ troubleshooting và phân tích hoạt động.

2. **CloudWatch Metrics**: Theo dõi mức sử dụng tài nguyên của ECS và hoạt động connection của Application Load Balancer.

## Kiến trúc Monitoring

```text
                    Game Server
                         │
              ┌──────────┴──────────┐
              │                     │
          Container Logs       Runtime Metrics
              │                     │
              ▼                     ▼
      CloudWatch Logs       CloudWatch Metrics
              │                     │
              └──────────┬──────────┘
                         ▼
                CloudWatch Dashboard
                         │
              ┌──────────┴──────────┐
              │                     │
        Log Monitoring       Performance Monitoring