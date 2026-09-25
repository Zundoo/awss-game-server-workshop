---
title: "4.1.3. Internet Gateway"
weight: 413
---

# 4.1.3. Configuring Internet Gateway (IGW)

*   **Objective**: Enable resources located within the Public Subnets (such as the ALB) to communicate bidirectionally with the public Internet.
*   **Step-by-Step Implementation**:
    1. From the left VPC menu, select **Internet gateways** > click **Create internet gateway**.
    2. Enter the Name tag: `game-server-igw` > click **Create**.
    3. Select the newly created IGW > click **Actions** > select **Attach to VPC** > search and attach it to `game-server-vpc`.
