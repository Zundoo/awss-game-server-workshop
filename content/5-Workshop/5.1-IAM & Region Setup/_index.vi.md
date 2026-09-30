---
title: "IAM & Cấu hình Region"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 5.1 </b> "
---

# IAM & CẤU HÌNH REGION

Phần này chuẩn bị môi trường AWS trước khi triển khai hạ tầng Real-time Game Server.

Các mục tiêu chính bao gồm lựa chọn AWS Region, cấu hình môi trường AWS và chuẩn bị các quyền IAM cần thiết cho những dịch vụ được sử dụng trong Workshop.

## 5.1.1. Lựa chọn AWS Region

Toàn bộ tài nguyên trong Workshop được triển khai trong cùng một AWS Region.

Trong Workshop này, sử dụng:

```text
Region: Asia Pacific (Singapore)
Region Code: ap-southeast-1