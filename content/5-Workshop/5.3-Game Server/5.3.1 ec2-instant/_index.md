---
title : "EC2 Instance"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.3.1 </b> "
---

## EC2 Instance

**Objective:** Create a compute instance to host the real-time WebSocket Game Server.

### Step-by-Step Implementation

1. Navigate to **EC2** → **Instances** → **Launch instances**.

2. Configure the following parameters:

   - **Name**: `game-server-01`
   - **AMI**: Amazon Linux 2023
   - **Instance type**: `t3.medium` (or `t3.small`)
   - **Key pair**: Select or create a key pair
   - **Network settings**:
     - VPC: `game-server-vpc`
     - Subnet: `Private-Subnet-1A` (Private Subnet)
     - Auto-assign public IP: **Disable**
     - Security group: `sg-game-server`
   - **Storage**: 20–30 GB gp3

3. Click **Launch instance**.

   ![Launch EC2 Instance](/images/5/5.2/ec2-launch.png?featherlight=false&width=90pc)

4. Attach an IAM Role with the `AmazonSSMManagedInstanceCore` policy to enable Session Manager access.

5. Connect to the instance using **Session Manager**.

   ![EC2 Connected via Session Manager](/images/5/5.2/ec2-ssm.png?featherlight=false&width=90pc)