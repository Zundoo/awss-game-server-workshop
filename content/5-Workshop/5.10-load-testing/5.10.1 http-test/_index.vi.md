---
title : "Kiểm thử HTTP"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.10.1 </b> "
---

# 5.10.1. Kiểm thử HTTP Health Check Endpoint

**Mục tiêu:** Đánh giá tính ổn định và hiệu năng phản hồi của API endpoint `/health` khi liên tục nhận các HTTP Health Check Request từ Application Load Balancer.

## Quy trình kiểm thử

Gửi liên tục các HTTP Request đến endpoint `/health` thông qua Application Load Balancer.

Luồng Request được thực hiện như sau:

```text
Client / Test Tool
       ↓
Application Load Balancer
       ↓
Target Group
       ↓
ECS Fargate Task
       ↓
Game Server :8080
       ↓
/health