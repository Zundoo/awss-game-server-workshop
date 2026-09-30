---
title : "Task Definition"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.5.2 </b> "
---

## Registering ECS Task Definition

**Objective:** Create a task definition that specifies the compute resources, container image, network configuration, and environment variables required to run the Game Server on Amazon ECS.

## Core Configuration Parameters

1. **Task definition family**: `game-server-task`

2. **Launch type**: `AWS Fargate`

3. **Task size**:
   - **CPU**: `0.25 vCPU`
   - **Memory**: `0.5 GB`

   This minimal resource profile is suitable for the Workshop environment and helps reduce infrastructure costs.

4. **Container details**:

   - **Name**: `game-server`
   - **Image URI**:

     ```text
     <AWS_ACCOUNT_ID>.dkr.ecr.ap-southeast-1.amazonaws.com/game-server:latest
     ```

   - **Port mappings**:
     - **Container port**: `8080`
     - **Protocol**: `TCP`

5. **Environment variables**:

   Configure the Redis connection parameters required by the Game Server:

   | Variable | Value |
   |---|---|
   | `REDIS_HOST` | `<REDIS_ENDPOINT>` |
   | `REDIS_PORT` | `6379` |
   | `REDIS_TLS` | `true` |

   ![Container and Environment Variables Setup in Task Definition](/images/5/5.5/5.5.2/0001.png?featherlight=false&width=90pc)

6. Review the task definition configuration and click **Create**.

After the task definition is registered, the `game-server-task` revision can be used by an ECS Service to launch the Game Server containers on AWS Fargate.