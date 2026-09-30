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

   ![Creating Public Route Table](images/5/5.2/rtpublic.png?featherlight=false&width=90pc)

3. Select `game-public-rt` > open the **Routes** tab > click **Edit routes**.

4. Add the following route:

   - **Destination**: `0.0.0.0/0`
   - **Target**: Internet Gateway (`game-server-igw` or the IGW attached to the VPC)

   This route allows resources in the associated Public Subnets (ALB, NAT Gateway) to communicate with the public Internet through the Internet Gateway.

   ![Public Route Table - Routes configuration](images/5/5.2/rtpublic2.png?featherlight=false&width=90pc)

5. Open the **Subnet associations** tab > click **Edit subnet associations**.

6. Select the following Public Subnets:

   - `game-public-1a` (or `Public-Subnet-1A`)
   - `game-public-1b` (or `Public-Subnet-1B`)

   Click **Save associations**.

   ![Public Route Table - Subnet Associations](images/5/5.2/rtpulic3.png?featherlight=false&width=90pc)

### 2. Private Route Table

Create a separate Route Table named `game-private-rt` for the Private Subnets.

1. From the **Route tables** page, click **Create route table**.

2. Configure the following parameters:

   - **Name**: `game-private-rt`
   - **VPC**: `game-server-vpc`

   ![Creating Private Route Table](images/5/5.2/rtprivate.png?featherlight=false&width=90pc)
3. Keep the default **Local** route:

   - **Destination**: `10.0.0.0/16`
   - **Target**: `local`

4. Add the following route (important for outbound internet access via NAT):

   - **Destination**: `0.0.0.0/0`
   - **Target**: NAT Gateway (the NAT Gateway created in the Public Subnet)

   This route allows resources in the Private Subnets (EC2 Game Server, RDS, Redis) to access the Internet **through the NAT Gateway** (for pulling Docker images, SSM Agent, package updates, etc.) while remaining unreachable directly from the public Internet.

   ![Private Route Table - Routes with NAT Gateway](images/5/5.2/rtprivate2.png?featherlight=false&width=90pc)

5. Open the **Subnet associations** tab > click **Edit subnet associations**.

6. Select the following Private Subnets:

   - `game-private-1a` (or `Private-Subnet-1A`)
   - `game-private-1b` (or `Private-Subnet-1B`)

   Click **Save associations**.

   ![Private Route Table - Subnet Associations](images/5/5.2/rtprivate3.png?featherlight=false&width=90pc)
After completing the configuration:

- Public Subnets use `game-public-rt` → traffic goes out via **Internet Gateway**.
- Private Subnets use `game-private-rt` → traffic goes out via **NAT Gateway** (no direct route to Internet Gateway).

This design keeps the Game Server, RDS and Redis private while still allowing necessary outbound connectivity.
