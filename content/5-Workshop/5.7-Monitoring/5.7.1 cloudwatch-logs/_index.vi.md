---

title : "CloudWatch Logs"

date : "`r Sys.Date()`"

weight : 1

chapter : false

pre : " <b> 5.7.1 </b> "

---

## Cấu hình tập trung Log với CloudWatch Logs

**Mục tiêu:** Tập trung các log của các container Game Server vào **Amazon CloudWatch Logs** để theo dõi hoạt động theo thời gian thực, hỗ trợ kiểm tra lỗi và phân tích hoạt động của hệ thống.

Trong kiến trúc **Real-time Game Server**, các log được tạo từ container ECS Fargate sẽ được thu thập và gửi đến **Amazon CloudWatch Logs** thông qua cấu hình log collection của ECS.

## Các bước cấu hình

1. Truy cập **Amazon ECS** > **Task Definitions**.

2. Chọn Task Definition của Game Server:

   `game-server-task`

3. Tạo một **Task Definition revision** mới hoặc cập nhật revision hiện tại.

4. Mở phần cấu hình **Container** của container:

   `game-server`

5. Bật tùy chọn **Log collection**.

6. Cấu hình **Amazon CloudWatch** làm nơi lưu trữ log với các thông số:

   - **Destination:** `Amazon CloudWatch`
   - **Log group:** `/ecs/game-server-task`
   - **Create log group:** `true`
   - **AWS Region:** `ap-southeast-1`
   - **Stream prefix:** `ecs`

   ![Cấu hình CloudWatch Logs cho ECS Container](/awss-game-server-workshop/static/images/5/5.8/cloud2.png?featherlight=false&width=90pc)

7. Kiểm tra **ECS Task Execution Role** có đầy đủ quyền để gửi log của container đến CloudWatch Logs.

   Policy AWS-managed thường được sử dụng cho mục đích này:

   `AmazonECSTaskExecutionRolePolicy`

8. Đăng ký **Task Definition revision** mới.

9. Cập nhật **ECS Service** để sử dụng revision mới.

10. Chờ Game Server Fargate Task chuyển sang trạng thái:

   `RUNNING`

## Kiểm tra CloudWatch Logs

Sau khi Game Server Task khởi động thành công:

1. Truy cập **Amazon CloudWatch**.

2. Chọn:

   **Logs** → **Log groups**

3. Mở Log Group:

   `/ecs/game-server-task`

4. Kiểm tra ECS đã tạo **Log Stream**.

5. Mở Log Stream và kiểm tra các thông tin được ghi nhận từ Game Server container.

   ![Kiểm tra CloudWatch Log Stream](/awss-game-server-workshop/static/images/5/5.8/cloudlog2.png?featherlight=false&width=90pc)


## Kiểm tra Log của Real-time Game Server

Do workshop triển khai **Real-time Game Server sử dụng WebSocket**, CloudWatch Logs có thể được sử dụng để theo dõi các sự kiện trong quá trình Game Server hoạt động, chẳng hạn:

- Khởi động Game Server.
- Client kết nối đến Game Server.
- Client ngắt kết nối.
- Message được nhận từ Client.
- Message được gửi đến Client.
- Hoạt động của Player hoặc Session.
- Lỗi xảy ra trong ứng dụng.
- Lỗi xử lý kết nối WebSocket.

Ví dụ, khi thực hiện kiểm thử bằng **Artillery**, Game Server có thể ghi nhận các log như:

```text
Received: hello from Artillery!
Received: hello from Artillery!
Received: hello from Artillery!