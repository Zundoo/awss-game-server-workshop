---
title : "Route Tables"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 5.2.4 </b> "
---

## Establishing Route Tables

The system uses two separate Route Tables to control traffic between the Public and Private Subnets.

### 1. Public Route Table

Create a Route Table named `game-public-rt` for the Public Subnets.

1. From the VPC Console, select **Route tables** > click **Create route table**.

2. Configure the following parameters:

   - **Name**: `game-public-rt`
   - **VPC**: `game-server-vpc`

   ![Creating Public Route Table](/images/5/5.2/5.2.4/0001.png?featherlight=false&width=90pc)

3. Select `game-public-rt` > open the **Routes** tab > click **Edit routes**.

4. Add the following route:

   - **Destination**: `0.0.0.0/0`
   - **Target**: `game-server-igw`

   This route allows resources in the associated Public Subnets to communicate with the public Internet through the Internet Gateway.

   ![Public Route Table Configuration](/images/5/5.2/5.2.4/0002.png?featherlight=false&width=90pc)

5. Open the **Subnet associations** tab > click **Edit subnet associations**.

6. Select the following Public Subnets:

   - `Public-Subnet-1A`
   - `Public-Subnet-1B`

   Click **Save associations**.

   ![Public Subnet Associations](/images/5/5.2/5.2.4/0003.png?featherlight=false&width=90pc)

### 2. Private Route Table

Create a separate Route Table named `game-private-rt` for the Private Subnets.

1. From the **Route tables** page, click **Create route table**.

2. Configure the following parameters:

   - **Name**: `game-private-rt`
   - **VPC**: `game-server-vpc`

3. Keep the default **Local** route:

   - **Destination**: `10.0.0.0/16`
   - **Target**: `local`

   No route to the Internet Gateway is configured for this Route Table. This prevents resources in the Private Subnets from directly accessing the public Internet.

4. Open the **Subnet associations** tab > click **Edit subnet associations**.

5. Select the following Private Subnets:

   - `Private-Subnet-1A`
   - `Private-Subnet-1B`

   Click **Save associations**.

   ![Private Route Table and Subnet Associations](/images/5/5.2/5.2.4/0004.png?featherlight=false&width=90pc)

After completing the configuration, the Public Subnets use `game-public-rt` to access the Internet through the Internet Gateway, while the Private Subnets use `game-private-rt` and do not have a direct route to the Internet Gateway.