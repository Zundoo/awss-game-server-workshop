---
title : "5.2.2. Subnets"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.2.2 </b> "
---

## Subnet Segmentation

To optimize security using a **3-Tier Architecture**, the network is segmented into Public and Private subnets distributed across at least 2 Availability Zones (AZs):

### Public Subnets

**Inbound Internet Traffic:**

- `Public-Subnet-1A` (CIDR: `10.0.1.0/24`) in AZ `ap-southeast-1a`.

- `Public-Subnet-1B` (CIDR: `10.0.2.0/24`) in AZ `ap-southeast-1b`.

### Private Subnets

**Isolated Compute & Database Plane:**

- `Private-Subnet-1A` (CIDR: `10.0.11.0/24`) in AZ `ap-southeast-1a`.

- `Private-Subnet-1B` (CIDR: `10.0.12.0/24`) in AZ `ap-southeast-1b`.