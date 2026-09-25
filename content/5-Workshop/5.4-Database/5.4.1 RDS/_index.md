---
title : "RDS"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.4.1 </b> "
---

## Provisioning Amazon RDS Instance

**Objective:** Deploy a relational database system to securely store player metadata, match histories, and persistent inventory data.

## Configuration Architecture

1. Navigate to **Amazon RDS** > select **Databases** > click **Create database**.

2. Select **Standard create** and configure the database engine:
   - **Engine type**: `MySQL`
   - PostgreSQL may be selected instead if it matches the application's project stack.

3. Under **Templates**, select **Free tier** to minimize workshop costs.

4. Configure the database connectivity settings:
   - **VPC**: Select `game-server-vpc`.
   - Configure the DB subnet group to use the **Private Subnets**.
   - Do not place the database directly in a Public Subnet.

   ![RDS Connectivity Configuration](/images/5/5.4/5.4.1/0001.png?featherlight=false&width=90pc)

5. Configure the database instance according to the workshop requirements and review the settings.

6. Click **Create database**.

After the database is provisioned, the RDS instance will operate inside the VPC and remain isolated from direct public Internet access. The Game Server application can communicate with the database through the private network using the appropriate Security Group rules.