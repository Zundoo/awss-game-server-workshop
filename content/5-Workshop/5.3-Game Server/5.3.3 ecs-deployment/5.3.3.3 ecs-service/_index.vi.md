---
title : "ECS Service"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 5.5.3 </b> "
---

## Triển khai Runtime thông qua ECS Service

**Mục tiêu:** Triển khai và duy trì số lượng Game Server Task ổn định bên trong môi trường Private Subnet được cô lập.

## Các bước cấu hình

1. Truy cập **Amazon ECS** > **Clusters** và chọn `game-server-cluster`.

2. Tại tab **Services**, nhấn **Create**.

3. Cấu hình Deployment:

   - **Task definition**: Chọn `game-server-task`.
   - **Revision**: Chọn revision mới nhất.
   - **Desired tasks**: Đặt giá trị `1` cho lần triển khai ban đầu.

4. Cấu hình **Networking**:

   - **VPC**: Chọn `game-server-vpc`.
   - **Subnets**:
     - `Private-Subnet-1A`
     - `Private-Subnet-1B`
   - **Security group**: Chọn `game-server-sg`.

   ![Cấu hình Networking cho ECS Service](/images/5/5.5/5.5.3/0001.png?featherlight=false&width=90pc)

5. Kiểm tra lại cấu hình Service và nhấn **Create**.

6. Mở ECS Service vừa tạo và chuyển đến tab **Tasks**.

7. Kiểm tra Task đã được khởi chạy thành công và trạng thái hiển thị là **Running**.

   ![Trạng thái ECS Service Running Tasks](/images/5/5.5/5.5.3/0002.png?featherlight=false&width=90pc)

Sau khi Service được triển khai thành công, Amazon ECS sẽ duy trì số lượng Task theo giá trị **Desired tasks** đã cấu hình. Các Game Server container hoạt động bên trong Private Subnets và được bảo vệ bởi Security Group `game-server-sg`.