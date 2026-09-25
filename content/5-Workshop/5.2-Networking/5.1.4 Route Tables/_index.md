---
title: "4.1.4. Route Tables"
weight: 414
---

# 4.1.4. Establishing Route Tables

The system configures two distinct route tables to strict control network traffic mapping:

1.  **Public Route Table** (`game-public-rt`):
    *   Add a route: **Destination `0.0.0.0/0` \(\rightarrow\) Target: `game-server-igw`**.
    *   Explicitly associate with 2 subnets: `Public-Subnet-1A` and `Public-Subnet-1B`.
2.  **Private Route Table** (`game-private-rt`):
    *   Keep the default local routing configuration only (`Local`), with no route to the Internet Gateway to ensure absolute security.
    *   Explicitly associate with 2 subnets: `Private-Subnet-1A` and `Private-Subnet-1B`.
