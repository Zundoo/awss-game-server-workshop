---
title : "Docker Installation"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.3.2 </b> "
---

## Cài đặt Docker

**Mục tiêu:** Cài đặt Docker và Docker Compose trên EC2 instance để chạy container Game Server.

### Các bước thực hiện

1. Cập nhật hệ thống và cài đặt Docker:

```bash
sudo dnf update -y
sudo dnf install -y docker
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker ec2-user