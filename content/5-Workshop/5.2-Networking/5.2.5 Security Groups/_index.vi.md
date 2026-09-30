---
title : "Security Groups"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 5.2.5 </b> "
---

## Quản lý luật tường lửa (Security Groups)

Security Groups đóng vai trò như các **tường lửa ảo có lưu trạng thái (stateful)** giúp kiểm soát lưu lượng truy cập đầu vào (inbound) và đầu ra (outbound) cho các tài nguyên AWS.

Đối với hạ tầng Game Server, các Security Group được cấu hình theo **Nguyên tắc đặc quyền tối thiểu (Principle of Least Privilege)**, chỉ cho phép các luồng truy cập thực sự cần thiết bởi từng thành phần.

Các Security Group chính được sử dụng trong bài thực hành này bao gồm:

| Security Group | Tài nguyên | Mục đích |
|---|---|---|
| `alb-sg` | Application Load Balancer | Cho phép client công cộng truy cập (HTTP/HTTPS/WebSocket) |
| `game-server-sg` | Game Server / ECS / EC2 | Cho phép nhận dữ liệu từ ALB và quản trị hệ thống |
| `rds-sg` | Relational Database Service | Chỉ cho phép các Game Server truy cập vào cơ sở dữ liệu |
| `redis-sg` | ElastiCache / Redis | Chỉ cho phép các Game Server truy cập bộ nhớ đệm và Pub/Sub |
| `bastion-sg` | Bastion Host (Khuyến nghị) | Cung cấp cổng truy cập SSH an toàn để quản trị |

---

## 1. ALB Security Group

Tạo một Security Group tên là `alb-sg` cho **Application Load Balancer**.

ALB là cổng vào công cộng duy nhất của hạ tầng Game Server. Nó tiếp nhận các kết nối từ client bên ngoài Internet và chuyển tiếp (forward) lưu lượng truy cập xuống Game Server đang chạy trong Private Subnet.

### Inbound Rules

Cấu hình các luật inbound sau:

| Loại | Giao thức | Khoảng Port | Nguồn | Mô tả / Mục đích |
|---|---|---:|---|---|
| HTTP | TCP | `80` | `0.0.0.0/0` | HTTP (Tự động chuyển hướng sang HTTPS) |
| HTTPS | TCP | `443` | `0.0.0.0/0` | HTTPS + WebSocket (WSS) |
| Custom TCP | TCP | `8080` | `0.0.0.0/0` | (Tùy chọn) Nếu bạn sử dụng một port WebSocket riêng biệt |

Nguồn `0.0.0.0/0` cho phép mọi client từ Internet có thể tiếp cận bộ cân bằng tải ALB.

### Outbound Rules
* **All traffic** → `0.0.0.0/0` (Mặc định)

![ALB Security Group Inbound Rules](images/5/5.2/sgalb2.png?featherlight=false&width=90pc)

> **Lưu ý:** ALB sẽ điều hướng các kết nối WebSocket từ port 443 (hoặc 80) xuống Target Group của Game Server (thường chạy trên port 8080 hoặc 3000 của các thực thể EC2/ECS).

---

## 2. Game Server Security Group

Tạo một Security Group tên là `game-server-sg` cho các tài nguyên Game Server.

Do Game Server nằm bên trong **Private Subnet**, nó tuyệt đối không được phép tiếp nhận truy cập trực tiếp từ Internet công cộng.

### Inbound Rules

Cấu hình các luật đầu vào dựa trên môi trường của Game Server:

| Loại | Giao thức | Khoảng Port | Nguồn | Mô tả / Mục đích |
|---|---|---:|---|---|
| Custom TCP | TCP | `8080` | `alb-sg` | Kết nối WebSocket gửi từ ALB (Quan trọng nhất) |
| Custom TCP | TCP | `3000` | `alb-sg` | Lưu lượng ứng dụng/dịch vụ (Nếu app sử dụng port 3000) |
| HTTP | TCP | `80` | `alb-sg` | Kiểm tra trạng thái (Health check) / HTTP (Nếu cần) |
| SSH | TCP | `22` | `Your-IP/32` hoặc `bastion-sg` | Truy cập quản trị hệ thống EC2 |
| Custom TCP | TCP | `8080` | `game-server-sg` | (Tùy chọn) Giao tiếp nội bộ giữa các server với nhau |

### Outbound Rules
* **All traffic** → `0.0.0.0/0`
* *(Hoặc cấu hình nghiêm ngặt hơn: Chỉ cho phép kết nối đầu ra đi tới `rds-sg`, `redis-sg`, và ra Internet để tải các Docker image).*

![Game Server Security Group Inbound Rules](images/5/5.2/sggme.png?featherlight=false&width=90pc)

Luật chạy ứng dụng chính cấu hình như sau:

```text
Type:   Custom TCP
Port:   8080
Source: alb-sg
```

---

## 3. RDS Security Group

Tạo một Security Group tên là `rds-sg` cho **Relational Database Service (RDS)**.

### Inbound Rules

| Loại | Giao thức | Khoảng Port | Nguồn | Mô tả / Mục đích |
|---|---|---:|---|---|
| MySQL/Aurora | TCP | `3306` | `game-server-sg` | Chỉ cho phép duy nhất Game Server truy cập cơ sở dữ liệu |
| PostgreSQL | TCP | `5432` | `game-server-sg` | (Nếu hệ thống sử dụng PostgreSQL) |

### Outbound Rules

* **All traffic** → `0.0.0.0/0` (Hoặc giữ lại các luật mặc định nếu cần)

> **Cảnh báo bảo mật nghiêm trọng:** Không bao giờ được mở các luật inbound của RDS Security Group ra phạm vi công cộng `0.0.0.0/0`.

---

## 4. Redis Security Group

Tạo một Security Group tên là `redis-sg` cho cụm **Redis / ElastiCache**.

### Inbound Rules

| Loại | Giao thức | Khoảng Port | Nguồn | Mô tả / Mục đích |
|---|---|---:|---|---|
| Custom TCP | TCP | `6379` | `game-server-sg` | Truy cập Redis (Bộ nhớ đệm + Pub/Sub cho WebSocket) |

### Outbound Rules

* **All traffic** → `0.0.0.0/0`

---

## 5. Bastion Host Security Group

Tạo một Security Group tên là `bastion-sg` để thiết lập **Cổng kết nối SSH an toàn** vào hạ tầng mạng riêng tư của bạn.

### Inbound Rules

| Loại | Giao thức | Khoảng Port | Nguồn | Mô tả / Mục đích |
|---|---|---:|---|---|
| SSH | TCP | `22` | `Your-IP/32` | Giới hạn quyền SSH duy nhất từ địa chỉ IP tĩnh công cộng của bạn |

### Outbound Rules
* **All traffic** → `0.0.0.0/0`

> **Thực hành tốt nhất (Best Practice):** Khi sử dụng Bastion Host, bạn hãy cấu hình luật SSH (Port 22) tại `game-server-sg` sao cho **chỉ chấp nhận** nguồn từ `bastion-sg` thay vì dùng IP cá nhân trực tiếp.
