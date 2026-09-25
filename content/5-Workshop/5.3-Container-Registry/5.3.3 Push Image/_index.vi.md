
### Vietnamese — `5.3.3 Push Image`

```markdown
---
title : "Push Image"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 5.3.3 </b> "
---

## Đẩy Docker Image lên Amazon ECR

Sau khi tạo ECR Repository và cấu hình Dockerfile, tiến hành build Docker Image của Game Server và đẩy image lên Private Repository trên Amazon ECR.

## Các bước thực hiện

Mở terminal tại thư mục gốc của project Game Server và thực hiện lần lượt các lệnh sau.

### 1. Xác thực Docker với Amazon ECR

Xác thực Docker CLI với Private ECR Registry:

```bash
aws ecr get-login-password --region ap-southeast-1 | docker login --username AWS --password-stdin <AWS_ACCOUNT_ID>.dkr.ecr.ap-southeast-1.amazonaws.com