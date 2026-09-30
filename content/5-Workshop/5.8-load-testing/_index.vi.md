---
title: "Kiểm thử tải"
weight: 9
chapter: false
pre: " <b> 5.10 </b> "
---

# KIỂM THỬ TẢI VÀ STRESS TEST HẠ TẦNG

Phần này trình bày các chỉ số kỹ thuật và kết quả phân tích hiệu năng được thu thập trong quá trình Stress Test hạ tầng bằng **Artillery**.

Quá trình kiểm thử đánh giá khả năng hoạt động của kiến trúc Real-time Game Server dưới tải đồng thời cao, với kịch bản mô phỏng tối đa **1.000 WebSocket Connection đồng thời**.

## Phạm vi kiểm thử

Quá trình Load Testing tập trung đánh giá các thành phần hạ tầng sau:

- **Application Load Balancer** — Tiếp nhận các kết nối từ Client và phân phối Traffic đến các ECS Task.

- **Amazon ECS / AWS Fargate** — Chạy Game Server Application dưới dạng Container.

- **WebSocket Server** — Duy trì các kết nối Client liên tục và xử lý các Message theo thời gian thực.

- **ECS Service Auto Scaling** — Phản ứng với mức sử dụng tài nguyên tăng bằng cách điều chỉnh số lượng Task đang chạy.

- **Amazon CloudWatch** — Cung cấp các Metric để theo dõi mức sử dụng tài nguyên, số lượng Connection và trạng thái hệ thống.

## Quy trình Load Testing

Traffic kiểm thử đi qua kiến trúc:

```text
Artillery Load Generator
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