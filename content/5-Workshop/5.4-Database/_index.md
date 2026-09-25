---
title : "Database"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 5.4 </b> "
---

## Database & Cache Tier Provisioning

This section covers the provisioning of the persistent database and in-memory cache layers required by the **Real-time Game Server**.

**Amazon RDS** is used to store persistent game data such as player metadata, match histories, and inventory states, while **Amazon ElastiCache for Redis** provides a low-latency in-memory data layer for real-time session state and frequently accessed game data.

## Implementation Overview

1. **Amazon RDS**: Provision a relational database inside the private network to store persistent Game Server data.

2. **Amazon ElastiCache for Redis**: Provision a Redis cluster to provide low-latency access to temporary session and real-time game state data.

3. **Network Security**: Restrict database and cache access to authorized Game Server resources through Security Groups and private network connectivity.

## Database Architecture

The database and cache tier is isolated from direct public Internet access:

```text
              Game Server
                   │
          ┌────────┴────────┐
          │                 │
          ▼                 ▼
      Amazon RDS      ElastiCache Redis
     Persistent Data    Session / Cache
          │                 │
          └──── Private ────┘
               Network