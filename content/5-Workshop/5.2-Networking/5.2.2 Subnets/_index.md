---
title : "Subnets"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.2.2 </b> "
---

## Subnet Segmentation

To optimize security using a **3-Tier Architecture**, the network is segmented into Public and Private subnets distributed across at least 2 Availability Zones (AZs).

### Public Subnets

**Purpose:** Host resources that need direct inbound access from the Internet (Application Load Balancer, NAT Gateway).

- `Public-Subnet-1A` (CIDR: `10.0.1.0/24`) in AZ `ap-southeast-1a`
- `Public-Subnet-1B` (CIDR: `10.0.2.0/24`) in AZ `ap-southeast-1b`

### Private Subnets

**Purpose:** Host internal resources that should not be directly accessible from the Internet (EC2 Game Server, RDS, ElastiCache Redis).

- `Private-Subnet-1A` (CIDR: `10.0.11.0/24`) in AZ `ap-southeast-1a`
- `Private-Subnet-1B` (CIDR: `10.0.12.0/24`) in AZ `ap-southeast-1b`

---

## Step-by-Step Implementation

1. From the VPC Console, select **Subnets** > click **Create subnet**.

2. Configure the following parameters for the first Public Subnet:

   - **VPC ID**: `game-server-vpc`
   - **Subnet name**: `Public-Subnet-1A`
   - **Availability Zone**: `ap-southeast-1a`
   - **IPv4 CIDR block**: `10.0.1.0/24`

   Click **Add new subnet** to continue creating the remaining subnets in the same wizard.

   ![Create Public Subnet 1A](images/5/5.2/subnet1.png?featherlight=false&width=90pc)

3. Create the second Public Subnet:

   - **Subnet name**: `Public-Subnet-1B`
   - **Availability Zone**: `ap-southeast-1b`
   - **IPv4 CIDR block**: `10.0.2.0/24`

4. Create the first Private Subnet:

   - **Subnet name**: `Private-Subnet-1A`
   - **Availability Zone**: `ap-southeast-1a`
   - **IPv4 CIDR block**: `10.0.11.0/24`

5. Create the second Private Subnet:

   - **Subnet name**: `Private-Subnet-1B`
   - **Availability Zone**: `ap-southeast-1b`
   - **IPv4 CIDR block**: `10.0.12.0/24`

   Click **Create subnet**.

   ![Create All Subnets](images/5/5.2/subnet2.png?featherlight=false&width=90pc)

6. (Optional but recommended) Enable **Auto-assign public IPv4 address** for the Public Subnets:

   - Select each Public Subnet → **Actions** → **Edit subnet settings**
   - Check **Enable auto-assign public IPv4 address** → Save

   ![Enable Auto-assign Public IP](images/5/5.2/subnet3.png?featherlight=false&width=90pc)

After completion, you should have 4 subnets as summarized below:

| Subnet Name          | CIDR            | Availability Zone   | Type    |
|----------------------|-----------------|---------------------|---------|
| Public-Subnet-1A     | 10.0.1.0/24     | ap-southeast-1a     | Public  |
| Public-Subnet-1B     | 10.0.2.0/24     | ap-southeast-1b     | Public  |
| Private-Subnet-1A    | 10.0.11.0/24    | ap-southeast-1a     | Private |
| Private-Subnet-1B    | 10.0.12.0/24    | ap-southeast-1b     | Private |

![Subnets Overview](images/5/5.2/subnet.png?featherlight=false&width=90pc)