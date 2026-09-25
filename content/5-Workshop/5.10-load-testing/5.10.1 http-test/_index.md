---
title : "HTTP Test"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.10.1 </b> "
---

# 5.10.1. Testing HTTP Health Check Endpoint Ingress

## Kiểm thử HTTP Health Check Endpoint

**Objective:** Measure the stability and response performance of the `/health` API endpoint under continuous HTTP health check requests from the Application Load Balancer.

**Mục tiêu:** Đánh giá tính ổn định và hiệu năng phản hồi của API endpoint `/health` khi liên tục nhận các HTTP Health Check Request từ Application Load Balancer.

## Test Procedure

### Quy trình kiểm thử

Send continuous HTTP requests to the `/health` endpoint through the Application Load Balancer.

Gửi liên tục các HTTP Request đến endpoint `/health` thông qua Application Load Balancer.

The request follows the application traffic path:

Request được thực hiện theo luồng:

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