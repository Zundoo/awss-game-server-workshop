---
title : "ECS Service"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 5.5.3 </b> "
---

## Deploying Runtime via ECS Service

**Objective:** Deploy and maintain a stable number of Game Server tasks within the isolated Private Subnet environment.

## Configuration Steps

1. Navigate to **Amazon ECS** > **Clusters** and select `game-server-cluster`.

2. Under the **Services** tab, click **Create**.

3. Configure the deployment:

   - **Task definition**: Select `game-server-task`.
   - **Revision**: Select the latest revision.
   - **Desired tasks**: Set to `1` for the initial deployment.

4. Configure the **Networking** settings:

   - **VPC**: Select `game-server-vpc`.
   - **Subnets**:
     - `Private-Subnet-1A`
     - `Private-Subnet-1B`
   - **Security group**: Select `game-server-sg`.

   ![ECS Service Networking Configuration](/images/5/5.5/5.5.3/0001.png?featherlight=false&width=90pc)

5. Review the Service configuration and click **Create**.

6. Open the newly created ECS Service and navigate to the **Tasks** tab.

7. Verify that the desired task has been successfully started and its status is **Running**.

   ![ECS Service Running Tasks Instance Status](/images/5/5.5/5.5.3/0002.png?featherlight=false&width=90pc)

After the Service is successfully deployed, Amazon ECS will maintain the configured desired task count. The Game Server containers run inside the Private Subnets and are protected by the `game-server-sg` Security Group.