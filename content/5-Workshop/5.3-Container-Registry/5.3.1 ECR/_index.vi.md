---
title : "ECR"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.3.1 </b> "
---

## Khởi tạo Amazon ECR Repository

**Mục tiêu:** Tạo một Private Repository trên Amazon Elastic Container Registry (ECR) để lưu trữ, quản lý và phiên bản hóa các Docker Image của Game Server một cách an toàn.

## Các bước thực hiện

1. Tìm kiếm và truy cập **Elastic Container Registry (ECR)** trên AWS Management Console.

2. Tại menu điều hướng bên trái, chọn **Repositories** > nhấn **Create repository**.

3. Cấu hình các thông số:

   - **Visibility settings**: Chọn **Private**.
   - **Repository name**: Nhập `game-server`.

   ![Tạo ECR Repository](/images/5/5.3/5.3.1/0001.png?featherlight=false&width=90pc)

4. Kiểm tra lại cấu hình và nhấn **Create repository**.

Sau khi Repository được tạo, `game-server` có thể được sử dụng để lưu trữ và quản lý các Docker Image của ứng dụng Game Server.

![ECR Repository đã được tạo](/images/5/5.3/5.3.1/0002.png?featherlight=false&width=90pc)