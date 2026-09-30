---
title : "Internet Gateway"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 5.2.3 </b> "
---

## Configuring Internet Gateway (IGW)

**Objective:** Enable resources located within the Public Subnets (such as the Application Load Balancer and NAT Gateway) to communicate with the public Internet.

## Step-by-Step Implementation

1. From the left-side VPC menu, select **Internet gateways** > click **Create internet gateway**.

2. Enter the following parameter:

   - **Name tag**: `game-server-igw`

   Click **Create internet gateway**.

   ![Create Internet Gateway](images/5/5.2/igw1.png?featherlight=false&width=90pc)
3. Select the newly created Internet Gateway (`game-server-igw`) > click **Actions** > select **Attach to VPC**.

4. Select `game-server-vpc` from the VPC list and click **Attach internet gateway**.

5. Verify the status:

   - The Internet Gateway should now show **State: Attached**
   - It is associated with `game-server-vpc`

   ![Internet Gateway Attached Successfully](images/5/5.2/igw2.png?featherlight=false&width=90pc)
The Internet Gateway is now attached to the `game-server-vpc` and can be used by resources in the Public Subnets to communicate with the Internet through the Public Route Table (`0.0.0.0/0` → Internet Gateway).