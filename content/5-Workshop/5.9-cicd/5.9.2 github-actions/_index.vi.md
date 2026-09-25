---
title: "4.8.2. GitHub Actions"
weight: 482
---

# 4.8.2. Cấu hình Kịch bản Tự động hóa GitHub Actions

Sinh viên tiến hành tạo file kịch bản tự động hóa đặt tại thư mục `.github/workflows/build-deploy.yml` để định nghĩa chuỗi hành động tự động đăng nhập AWS, tự động build Image và push trực tiếp lên kho chứa **Amazon ECR** khi có sự kiện đẩy code mới lên nhánh chính.

```yaml
name: Game Server CI/CD Pipeline
on:
  push:
    branches: [ master ]
jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout Code
      uses: actions/checkout@v4
    - name: Configure AWS Credentials
      uses: aws-actions/configure-aws-credentials@v4
      with:
        aws-access-key-id: \${{ secrets.AWS_ACCESS_KEY_ID }}
        aws-secret-access-key: \${{ secrets.AWS_SECRET_ACCESS_KEY }}
        aws-region: ap-southeast-1
```
