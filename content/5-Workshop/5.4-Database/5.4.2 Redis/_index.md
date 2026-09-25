---
title : "Redis"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.4.2 </b> "
---

## Configuring ElastiCache Redis

**Objective:** Deploy an **Amazon ElastiCache for Redis** cluster to handle Session data and support real-time game room state synchronization across multiple Game Servers.

Redis is deployed within the **Private Subnets** of `game-server-vpc` and only authorized Game Server resources are allowed to establish connections to Redis.

## ElastiCache Redis Configuration

1. Navigate to **Amazon ElastiCache** in the AWS Management Console.

2. Select **Redis caches** > click **Create Redis cache**.

3. Configure the Redis parameters according to the Workshop requirements.

4. Ensure that Redis is deployed within the Private network and uses a Security Group that allows connections from the Game Server.

   - **Redis Port**: `6379`
   - **VPC**: `game-server-vpc`
   - **Subnet**: Private Subnets

   ![ElastiCache Redis Configuration](/images/5/5.4/5.4.2/0001.png?featherlight=false&width=90pc)

---

## 🛠️ Troubleshooting Log: Resolving Redis Connection Issues Caused by TLS

### Issue

When testing the Redis connection from an EC2 instance using the standard Redis CLI command:

```bash
redis6-cli -h <REDIS_ENDPOINT> -p 6379