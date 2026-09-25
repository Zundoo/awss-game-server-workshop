---
title: "4.8.3. Deploy"
weight: 483
---

# 4.8.3. Triển khai Cập nhật Ứng dụng Không Gián Đoạn

*   **Mục tiêu**: Đẩy bản build Docker mới từ ECR xuống dịch vụ ECS Service để thay thế phiên bản ứng dụng cũ mà người chơi không hề bị ngắt kết nối đột ngột.
*   **Cơ chế thực thi**: Quy trình CI/CD kích hoạt lệnh cập nhật dịch vụ `aws ecs update-service`. 
*   **Kết quả**: Hệ thống ECS tự động áp dụng chiến thuật **Rolling Update** – khởi chạy một container mới thành công \(\rightarrow\) đăng ký vào ALB đạt trạng thái *Healthy* \(\rightarrow\) sau đó mới từ từ hủy container cũ chạy bản code lỗi thời, giúp quá trình bảo trì game diễn ra êm đẹp.

![Lịch sử luồng CI/CD chạy thành công hiển thị tích xanh trên GitHub](/images/4.8.3-deploy.png)
