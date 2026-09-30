---
title : "Redis"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.4.2 </b> "
---

## Configuring ElastiCache Redis

**Objective:** Deploy an **Amazon ElastiCache for Redis** cluster to handle session data and support real-time game room state synchronization across multiple Game Servers.

Redis is deployed within the **Private Subnets** of `game-server-vpc` and only authorized Game Server resources are allowed to establish connections to Redis.

## Step-by-Step Implementation

1. Navigate to **Amazon ElastiCache** → **Redis OSS caches** → **Create Redis OSS cache**.

2. Configure the following parameters:

   - **Deployment option**: Design your own cache
   - **Creation method**: Cluster cache
   - **Cluster mode**: Disabled
   - **Name**: `game-redis`
   - **Engine version**: 7.x (or latest available)
   - **Node type**: `cache.t3.micro` (or `cache.t4g.micro`)
   - **Number of replicas**: 0

3. Configure networking:

   - **Subnet group**: `game-redis-subnet-group` (Private Subnets)
   - **VPC**: `game-server-vpc`
   - **Security groups**: Select `sg-redis`
   - **Encryption in transit**: Disabled (for easier testing in the workshop)

   ![ElastiCache Redis Configuration](images/5/5.4/redis.png?featherlight=false&width=90pc)
4. Click **Create**.

5. Wait until the status becomes **Available** (usually 5–8 minutes).

6. Copy the **Primary endpoint**:
