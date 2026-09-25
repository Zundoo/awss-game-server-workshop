---
title : "Deploy"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 5.9.3 </b> "
---

## Triển khai phiên bản mới theo mô hình Rolling Update

**Mục tiêu:** Triển khai Docker Image mới từ Amazon ECR xuống ECS Service, thay thế các phiên bản Game Server cũ trong khi hạn chế tối đa gián đoạn đối với người dùng đang kết nối.

## Chiến lược triển khai

Sau khi GitHub Actions hoàn thành quá trình Build và Push Docker Image lên Amazon ECR, ECS Service có thể được yêu cầu triển khai phiên bản Image mới thông qua lệnh:

```bash
aws ecs update-service \
  --cluster game-server-cluster \
  --service game-server-service \
  --force-new-deployment \
  --region ap-southeast-1