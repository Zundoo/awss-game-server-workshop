---
title : "ECS Cluster"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.5.1 </b> "
---

## Creating Amazon ECS Cluster

**Objective:** Create a logical **Amazon Elastic Container Service (ECS)** cluster to manage and orchestrate Game Server container tasks.

## Configuration Steps

1. Navigate to **Amazon ECS** in the AWS Management Console.

2. Select **Clusters** > click **Create cluster**.

3. Configure the following parameters:

   - **Cluster name**: `game-server-cluster`
   - **Infrastructure**: Select **AWS Fargate**.

   AWS Fargate provides a serverless container execution environment, allowing the Game Server containers to run without directly managing the underlying EC2 instances.

   ![ECS Cluster Configuration](/images/5/5.5/5.5.1/0001.png?featherlight=false&width=90pc)

4. Review the configuration and click **Create**.

After the cluster is created, `game-server-cluster` will be available for deploying the Game Server container tasks through Amazon ECS.
   
![ECS Cluster Initialization Success](/images/5/5.5/5.5.1/0002.png?featherlight=false&width=90pc)