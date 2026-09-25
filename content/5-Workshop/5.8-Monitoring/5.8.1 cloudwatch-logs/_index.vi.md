---
title : "CloudWatch Logs"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.8.1 </b> "
---

## Cấu hình tập trung Log với CloudWatch Logs

**Mục tiêu:** Tập trung các log được tạo bởi Game Server container vào Amazon CloudWatch Logs để phục vụ giám sát, xử lý lỗi và phân tích hoạt động của hệ thống theo thời gian thực.

Log driver `awslogs` cho phép chuyển trực tiếp output của container đến một Log Group tập trung trên CloudWatch Logs.

## Các bước cấu hình

1. Truy cập **Amazon ECS** > **Task Definitions** và chọn:

   `game-server-task`

2. Tạo một revision mới hoặc cập nhật Task Definition hiện tại.

3. Mở cấu hình **Container** của:

   `game-server`

4. Cấu hình **Log collection** sử dụng `awslogs`:

   - **Log driver**: `awslogs`
   - **Log group**: `/aws/ecs/game-server`
   - **AWS Region**: `ap-southeast-1`
   - **Stream prefix**: `game-server`

   ![Cấu hình CloudWatch Logs cho ECS Container](/images/5/5.8/5.8.1/0001.png?featherlight=false&width=90pc)

5. Đảm bảo **Task Execution Role** của ECS Task có quyền tạo Log Stream và ghi Log Event vào CloudWatch Log Group đã cấu hình.

6. Đăng ký revision mới của Task Definition và cập nhật ECS Service để sử dụng revision này.

7. Sau khi Task mới khởi chạy thành công, truy cập:

   **Amazon CloudWatch** > **Logs** > **Log groups**

8. Mở Log Group:

   `/aws/ecs/game-server`

9. Kiểm tra Log Stream đã được tạo và log của container đang được ghi nhận.

   ![CloudWatch Logs Stream](/images/5/5.8/5.8.1/0002.png?featherlight=false&width=90pc)

## 🛠️ Case Study: Xử lý lỗi AccessDenied

### Hiện tượng

Log Group trên CloudWatch đã tồn tại nhưng phần **Log streams** vẫn không có dữ liệu, mặc dù Game Server container đã khởi chạy thành công.

### Nguyên nhân

**Task Execution Role** của ECS Task không có đủ quyền để tạo CloudWatch Log Stream và ghi Log Event.

### Cách xử lý

Kiểm tra IAM Role được sử dụng bởi ECS Task Definition.

Đối với cấu hình ECS `awslogs` tiêu chuẩn, Task Execution Role cần có các quyền cần thiết để thực hiện các thao tác với CloudWatch Logs. Các quyền này thường được cung cấp thông qua AWS-managed policy:

`AmazonECSTaskExecutionRolePolicy`

Sau khi cập nhật quyền IAM, triển khai lại ECS Service để Task mới được khởi chạy với Execution Role đã được cập nhật.

## Kiểm tra kết quả

Khi cấu hình chính xác, log của Game Server container sẽ xuất hiện trên CloudWatch Logs.

Các loại log có thể theo dõi bao gồm:

- Sự kiện khởi động Server
- Sự kiện Client kết nối và ngắt kết nối
- Trạng thái WebSocket connection
- Application errors
- Hoạt động của người chơi và thông tin Debug

Kiến trúc Logging:

```text
ECS Fargate Task
      │
      │ Container stdout / stderr
      ▼
  awslogs Driver
      │
      ▼
CloudWatch Log Group
/aws/ecs/game-server
      │
      ▼
 CloudWatch Logs