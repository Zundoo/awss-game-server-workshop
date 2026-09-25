---
title: "4.3.1. RDS"
weight: 431
---

# 4.3.1. Provisioning Amazon RDS Instance

*   **Objective**: Deploy a relational database system to securely store player metadata, match histories, and persistent inventory states.
*   **Configuration Architecture**:
    1. Navigate to **Amazon RDS** > select **Databases** > click **Create database**.
    2. Select **Standard create** > set Engine type to **MySQL** (or PostgreSQL depending on the project stack).
    3. Choose the **Free Tier** template to adhere to workshop budget guidelines.
    4. Connectivity settings: Select `game-server-vpc` and force subnets configuration strictly into the isolated **Private Subnets** network boundary to block external vector threats.
