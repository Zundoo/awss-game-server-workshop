---
title : "Tổng quan Workshop"
date : "`r Sys.Date()`"
weight : 1
chapter : true
pre : " <b> 5. </b> "
---

# AWS REAL-TIME GAME SERVER WORKSHOP

#### Tổng quan Workshop

Workshop này tập trung vào quá trình thiết kế, triển khai và kiểm thử hạ tầng Cloud dành cho **Game Server thời gian thực (Real-time Game Server)** hoạt động trên các kết nối **WebSocket** liên tục.

Workshop sử dụng hệ sinh thái **Amazon Web Services (AWS)** kết hợp với các công nghệ về mạng, bảo mật, container, cơ sở dữ liệu, cân bằng tải, giám sát và tự động mở rộng để xây dựng một hạ tầng Game Server có khả năng hoạt động ổn định và mở rộng khi số lượng người chơi tăng cao.

![Sơ đồ kiến trúc AWS Game Server tổng thể](/images/architecture-diagram.png?featherlight=false&width=90pc)

{{% notice info %}}

**Lưu ý về bảo mật:** Hạ tầng được thiết kế theo mô hình **3-Tier Architecture**, nhằm phân tách lớp truy cập bên ngoài, lớp ứng dụng và lớp dữ liệu. Các tài nguyên cung cấp dịch vụ ra Internet được đặt trong Public Subnets, trong khi các tài nguyên ứng dụng và cơ sở dữ liệu được cô lập trong Private Subnets.

{{% /notice %}}

#### Các dịch vụ AWS chính

* **Amazon VPC**: Xây dựng mạng ảo cô lập, cấu hình Subnet, Route Table và các cơ chế bảo mật mạng.

* **AWS IAM**: Quản lý người dùng, Role, quyền truy cập và cơ chế xác thực nhằm bảo vệ các tài nguyên AWS.

* **Amazon ECR & Docker**: Xây dựng, đóng gói và lưu trữ Docker Image của ứng dụng Game Server.

* **Amazon ECS**: Điều phối các container Game Server bằng AWS Fargate.

* **Application Load Balancer (ALB)**: Cung cấp điểm truy cập công khai và phân phối các kết nối WebSocket đến các container Game Server.

* **Amazon ElastiCache for Redis**: Cung cấp lớp dữ liệu trong bộ nhớ với độ trễ thấp để chia sẻ thông tin phiên chơi và trạng thái thời gian thực giữa các Game Server.

* **Amazon CloudWatch**: Thu thập các chỉ số hiệu năng của hệ thống và quản lý log tập trung của các container.

#### Mục tiêu của Workshop

Sau khi hoàn thành Workshop, bạn sẽ có thể:

1. Thiết kế kiến trúc mạng AWS an toàn và có khả năng mở rộng.

2. Cấu hình IAM và các cơ chế xác thực cho tài nguyên AWS.

3. Triển khai Game Server sử dụng WebSocket dưới dạng container thông qua Amazon ECS và AWS Fargate.

4. Cấu hình Redis làm lớp dữ liệu trong bộ nhớ cho ứng dụng thời gian thực.

5. Đưa Game Server ra Internet thông qua Application Load Balancer.

6. Cấu hình cơ chế Auto Scaling dựa trên mức sử dụng tài nguyên của ứng dụng.

7. Giám sát hiệu năng và log của các container bằng Amazon CloudWatch.

8. Thực hiện Load Testing để đánh giá khả năng xử lý của Game Server trong điều kiện có nhiều người dùng đồng thời.

#### Điều hướng nội dung Workshop

1. [5.1. IAM & Cấu hình khu vực](5.1-iam-regional/)

2. [5.2. Networking](5.2-networking/)