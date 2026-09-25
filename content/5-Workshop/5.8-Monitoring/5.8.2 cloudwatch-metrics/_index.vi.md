---
title: "4.7.2. CloudWatch Metrics"
weight: 472
---

# 4.7.2. Theo dõi Chỉ số Hiệu năng (CloudWatch Metrics)

*   **Mục tiêu**: Quản lý và theo dõi các biểu đồ hiệu năng phần cứng để phát hiện sớm các hiện tượng nghẽn mạch tài nguyên mạng hoặc quá tải vi xử lý.
*   **Các thông số trọng tâm cần giám sát**:
    1.  **CPUUtilization (Dịch vụ ECS)**: Tỷ lệ tiêu thụ CPU trung bình của cụm xử lý game.
    2.  **MemoryUtilization**: Tỷ lệ tiêu hao bộ nhớ RAM của hệ thống container.
    3.  **ActiveConnectionCount (Bộ cân bằng tải ALB)**: Tổng số lượng kết nối duy trì WebSocket thực tế từ người chơi đang cắm trực tiếp vào hệ thống.

![Biểu đồ giám sát chỉ số tài nguyên phần cứng hoạt động ổn định](/images/4.7.2-cloudwatch-metrics.png)
