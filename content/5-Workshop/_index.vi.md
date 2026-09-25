---
title : "Tổng quan Workshop"
date : "`r Sys.Date()`"
weight : 1
chapter : true
pre : " <b> 5. </b> "
---

# WORKSHOP AWS REAL-TIME GAME SERVER

#### Tổng quan Lab

Workshop này tập trung vào quá trình thiết kế kiến trúc, triển khai và kiểm thử hạ tầng Cloud dành cho **Real-time Game Server** hoạt động thông qua các kết nối **WebSocket** liên tục.

Workshop sử dụng hệ sinh thái **Amazon Web Services (AWS)** kết hợp với các công nghệ về Containerization, Networking, Security, Database, Load Balancing, Monitoring và Auto Scaling để xây dựng một hạ tầng Game Server có khả năng hoạt động ổn định và mở rộng.

![Sơ đồ kiến trúc AWS Game Server tổng thể](/images/architecture-diagram.png?featherlight=false&width=90pc)

{{% notice info %}}
**Lưu ý về bảo mật:** Hạ tầng được thiết kế theo mô hình **3-Tier Architecture** nhằm phân tách Public Access Layer, Application Layer và Data Layer. Các tài nguyên cần truy cập từ Internet được đặt trong Public Subnets, trong khi Application và Database Resources được cô lập trong Private Subnets.
{{% /notice %}}

#### Các dịch vụ AWS chính

- **Amazon VPC**: Xây dựng mạng Virtual Network độc lập, cấu hình Subnet, Route Table và Network Security.

- **AWS IAM**: Quản lý User, Role, Permission và các cơ chế Authentication để bảo vệ tài nguyên AWS.

- **Amazon ECR & Docker**: Build, Containerize và lưu trữ các Image của Game Server Application.

- **Amazon ECS**: Điều phối các Container Game Server Application sử dụng AWS Fargate.

- **Application Load Balancer (ALB)**: Cung cấp Public Entry Point và phân phối các WebSocket Connection đến các Game Server Container.

- **Amazon ElastiCache for Redis**: Cung cấp Data Layer trong bộ nhớ với độ trễ thấp để chia sẻ Game Session và Real-time State Information.

- **Amazon CloudWatch**: Thu thập các Application Metrics và Infrastructure Metrics, đồng thời quản lý Container Logs tập trung.

#### Mục tiêu Workshop

Sau khi hoàn thành Workshop, bạn sẽ học được cách:

1. Thiết kế AWS Network Architecture có tính bảo mật và khả năng mở rộng.

2. Cấu hình IAM và các cơ chế Authentication cho AWS Resources.

3. Triển khai Containerized WebSocket Game Server sử dụng Amazon ECS và AWS Fargate.

4. Cấu hình Redis làm In-memory Data Layer cho các ứng dụng Real-time.

5. Expose Game Server thông qua Application Load Balancer.

6. Cấu hình Auto Scaling dựa trên mức sử dụng tài nguyên của Application.

7. Giám sát hiệu năng Application và Container Logs bằng Amazon CloudWatch.

8. Thực hiện Load Testing để đánh giá Game Server trong điều kiện có số lượng Connection đồng thời cao.

#### Điều hướng triển khai Workshop

1. [5.1. IAM & Regional Configuration](5.1-iam-regional/)

2. [5.2. Networking](5.2-networking/)

3. [5.3. Container](5.3-container/)

4. [5.4. Database](5.4-database/)

5. [5.5. Game Server](5.5-game-server/)

6. [5.6. Load Balancing](5.6-load-balancing/)

7. [5.7. Scaling](5.7-scaling/)

8. [5.8. Monitoring](5.8-monitoring/)

9. [5.9. CI/CD](5.9-ci-cd/)

10. [5.10. Load Testing](5.10-load-testing/)