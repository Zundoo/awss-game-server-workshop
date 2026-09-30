---
title : "Security Groups"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 5.2.5 </b> "
---

## Firewall Rule Management (Security Groups)

Security Groups act as **stateful virtual firewalls** that control inbound and outbound traffic for AWS resources.

For the Game Server infrastructure, Security Groups are configured according to the **Principle of Least Privilege**, allowing only the traffic required by each component.

The main Security Groups used in this workshop are:

| Security Group | Resource | Purpose |
|---|---|---|
| `alb-sg` | Application Load Balancer | Allow public client traffic (HTTP/HTTPS/WebSocket) |
| `game-server-sg` | Game Server / ECS / EC2 | Allow traffic from the ALB and administration |
| `rds-sg` | Relational Database Service | Allow database access from Game Servers only |
| `redis-sg` | ElastiCache / Redis | Allow cache and Pub/Sub access from Game Servers only |
| `bastion-sg` | Bastion Host (Optional) | Provide secure administrative SSH access |

---

## 1. ALB Security Group

Create a Security Group named `alb-sg` for the **Application Load Balancer**.

The ALB is the public entry point of the Game Server infrastructure. It receives client connections and forwards traffic to the Game Server running in the Private Subnet.

### Inbound Rules

Configure the following inbound rules:

| Type | Protocol | Port Range | Source | Description / Purpose |
|---|---|---:|---|---|
| HTTP | TCP | `80` | `0.0.0.0/0` | HTTP (Redirect to HTTPS) |
| HTTPS | TCP | `443` | `0.0.0.0/0` | HTTPS + WebSocket (WSS) |
| Custom TCP | TCP | `8080` | `0.0.0.0/0` | (Optional) If exposing a dedicated WebSocket port |

The source `0.0.0.0/0` allows clients from the Internet to access the public-facing ALB.

### Outbound Rules

* **All traffic** → `0.0.0.0/0` (Default)

![ALB Security Group Inbound Rules](/awss-game-server-workshop/static/images/5/5.2/sgalb2.png?featherlight=false&width=90pc)

> **Note:** The ALB will forward WebSocket traffic from port 443 (or 80) down to the target group (typically port 8080 or 3000 on the EC2/ECS instances).

---

## 2. Game Server Security Group

Create a Security Group named `game-server-sg` for the Game Server resources.

The Game Server runs inside the **Private Subnet** and should not be directly accessible from the public Internet.

### Inbound Rules

Configure the following rules according to the Game Server environment:

| Type | Protocol | Port Range | Source | Description / Purpose |
|---|---|---:|---|---|
| Custom TCP | TCP | `8080` | `alb-sg` | WebSocket from ALB (Most important) |
| Custom TCP | TCP | `3000` | `alb-sg` | Application/service traffic (If app uses port 3000) |
| HTTP | TCP | `80` | `alb-sg` | Health check / HTTP traffic (If needed) |
| SSH | TCP | `22` | `Your-IP/32` or `bastion-sg` | EC2 Administrative access |
| Custom TCP | TCP | `8080` | `game-server-sg` | (Optional) Inter-server communication |

### Outbound Rules

* **All traffic** → `0.0.0.0/0` 
* *(Alternative restrictive approach: Restrict outbound traffic only to `rds-sg`, `redis-sg`, and the Internet for pulling Docker images).*

![Game Server Security Group Inbound Rules](/awss-game-server-workshop/static/images/5/5.2/sggme.png?featherlight=false&width=90pc)

The main application rule is:

```text
Type:   Custom TCP
Port:   8080
Source: alb-sg
```

---

## 3. RDS Security Group

Create a Security Group named `rds-sg` for the **Relational Database Service (RDS)**.

### Inbound Rules

| Type | Protocol | Port Range | Source | Description / Purpose |
|---|---|---:|---|---|
| MySQL/Aurora | TCP | `3306` | `game-server-sg` | Restrict database access to Game Servers only |
| PostgreSQL | TCP | `5432` | `game-server-sg` | (If using PostgreSQL) |

### Outbound Rules

* **All traffic** → `0.0.0.0/0` (Or retain only if explicitly required)

> **Critical Security Warning:** Never open the RDS Security Group inbound rules to `0.0.0.0/0`.

---

## 4. Redis Security Group

Create a Security Group named `redis-sg` for the **Redis / ElastiCache** cluster.

### Inbound Rules

| Type | Protocol | Port Range | Source | Description / Purpose |
|---|---|---:|---|---|
| Custom TCP | TCP | `6379` | `game-server-sg` | Redis access (Cache + WebSocket Pub/Sub) |

### Outbound Rules

* **All traffic** → `0.0.0.0/0`

---

## 5. Bastion Host Security Group (Recommended)

Create a Security Group named `bastion-sg` to enable **Secure SSH Access** to your private infrastructure.

### Inbound Rules

| Type | Protocol | Port Range | Source | Description / Purpose |
|---|---|---:|---|---|
| SSH | TCP | `22` | `Your-IP/32` | Restrict SSH access strictly to your public IP |

### Outbound Rules

* **All traffic** → `0.0.0.0/0`

> **Best Practice:** When utilizing a Bastion Host, ensure that the `game-server-sg` inbound rules for SSH (Port 22) **only** allow the `bastion-sg` as the source instead of any personal IP addresses.
