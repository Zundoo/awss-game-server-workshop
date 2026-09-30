---
title : "RDS"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.4.1 </b> "
---

## Provisioning Amazon RDS Instance

**Objective:** Deploy a relational database system to securely store player metadata, match histories, and persistent game data.

## Step-by-Step Implementation

1. Navigate to **Amazon RDS** → **Databases** → **Create database**.

2. Choose **Standard create** and configure the engine:

   - **Engine type**: `MySQL`
   - **Engine Version**: MySQL 8.0 (latest available)

3. Under **Templates**, select **Free tier** (or Dev/Test) to minimize costs.

4. Configure the database settings:

   - **DB instance identifier**: `game-db`
   - **Master username**: `admin`
   - **Master password**: Set a strong password (store it securely)

5. Configure **Connectivity**:

   - Select **Don’t connect to an EC2 compute resource**
   - **VPC**: `game-server-vpc`
   - **DB subnet group**: `game-db-subnet-group` (using Private Subnets)
   - **Public access**: **No**
   - **VPC security group**: Select existing → `sg-rds`

   ![RDS Connectivity Configuration](/awss-game-server-workshop/static/images/5/5.4/rdsconfic.png?featherlight=false&width=90pc)

6. Configure additional settings (optional):

   - Initial database name: `gamedb`
   - Disable automated backups if you want to reduce costs during the workshop

7. Click **Create database**.

   ![Create RDS Database](/awss-game-server-workshop/static/images/5/5.4/rds2.png?featherlight=false&width=90pc)

8. Wait until the status changes to **Available** (usually 5–10 minutes).

9. Copy the **Endpoint** for later use (example):
