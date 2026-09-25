---
title : "ECR"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.3.1 </b> "
---

## Initializing Amazon ECR Repository

**Objective:** Create an Amazon Elastic Container Registry (ECR) Private Repository to securely store, manage, and version the containerized Game Server images.

## Step-by-Step Implementation

1. Search for and navigate to **Elastic Container Registry (ECR)** in the AWS Management Console.

2. In the left navigation menu, select **Repositories** > click **Create repository**.

3. Configure the following parameters:

   - **Visibility settings**: Select **Private**.
   - **Repository name**: Enter `game-server`.

   ![Create ECR Repository](/images/5/5.3/5.3.1/0001.png?featherlight=false&width=90pc)

4. Review the configuration and click **Create repository**.

After the repository is created, the `game-server` repository can be used to store and manage Docker images for the Game Server application.

![ECR Repository Created](/images/5/5.3/5.3.1/0002.png?featherlight=false&width=90pc)