---
title : "GitHub Actions"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.9.2 </b> "
---

## Xây dựng quy trình CI/CD với GitHub Actions

**Mục tiêu:** Cấu hình GitHub Actions để tự động xác thực với AWS, xây dựng Docker Image của Game Server và đẩy Image lên Private Amazon ECR Repository mỗi khi có thay đổi được Push lên Branch `main`.

## Cấu hình Workflow

Tạo file Workflow tại:

```text
.github/workflows/build-deploy.yml

name: Game Server CI/CD Pipeline

on:
  push:
    branches: [ main ]

jobs:
  build-and-push:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ap-southeast-1

      - name: Login to Amazon ECR
        id: login-ecr
        uses: aws-actions/amazon-ecr-login@v2

      - name: Build, Tag, and Push Docker Image
        env:
          ECR_REGISTRY: ${{ steps.login-ecr.outputs.registry }}
          ECR_REPOSITORY: game-server
          IMAGE_TAG: ${{ github.sha }}
        run: |
          docker build -t $ECR_REGISTRY/$ECR_REPOSITORY:$IMAGE_TAG .
          docker push $ECR_REGISTRY/$ECR_REPOSITORY:$IMAGE_TAG