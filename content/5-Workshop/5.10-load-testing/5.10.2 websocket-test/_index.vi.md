---
title : "Kiểm thử WebSocket"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.10.2 </b> "
---

# 5.10.2. Kiểm thử tải WebSocket với số lượng kết nối đồng thời cao

Bài kiểm thử này đánh giá khả năng hoạt động của Real-time Game Server khi phải xử lý khối lượng WebSocket Traffic với số lượng kết nối đồng thời cao.

Công cụ kiểm thử tải **Artillery** được chạy từ máy local và gửi Traffic đến **Application Load Balancer DNS Hostname** công khai.

Bài kiểm thử mô phỏng tình huống số lượng người dùng tăng đột ngột bằng cách tạo **1.000 Virtual User trong khoảng 1 giây** và phát sinh **46.500 WebSocket Message** trong quá trình kiểm thử.

## Cấu hình kiểm thử

Các thông số của bài kiểm thử:

| Thông số | Giá trị |
|---|---:|
| Virtual Users | 1.000 |
| WebSocket Messages | 46.500 |
| WebSocket Send Rate | 1.629 messages/giây |
| Tổng thời gian kiểm thử | 35 giây |

Traffic kiểm thử đi qua luồng xử lý:

```text
Artillery
    ↓
Public ALB DNS
    ↓
Application Load Balancer
    ↓
Target Group
    ↓
ECS Fargate Tasks
    ↓
WebSocket Game Server