---
title: "Workshop Overview"
date: "`r Sys.Date()`"
weight: 1
chapter: true
pre: " <b> 5. </b> "
---

# AWS REAL-TIME GAME SERVER WORKSHOP

#### Lab Overview

This workshop focuses on the process of architecting, deploying, and testing a cloud infrastructure designed for a **Real-time Game Server** operating over persistent **WebSocket** connections.

The workshop uses the **Amazon Web Services (AWS)** ecosystem together with containerization, networking, security, database, load balancing, monitoring, and automated scaling technologies to build a reliable and scalable game server infrastructure.

![Overall AWS Game Server Architecture Diagram](/images/architecture-diagram.png?featherlight=false&width=90pc)

{{% notice info %}}

**Security Notice:**

The infrastructure follows a **3-Tier Architecture** to separate the public access layer, application layer, and data layer.

Public-facing resources are placed in Public Subnets, while application and database resources are isolated within Private Subnets.

{{% /notice %}}

#### Core AWS Services

- **Amazon VPC**: Building an isolated virtual network, configuring subnets, route tables, and network security.

- **AWS IAM**: Managing users, roles, permissions, and authentication mechanisms to secure AWS resources.

- **Amazon ECR & Docker**: Building, containerizing, and storing the Game Server application images.

- **Amazon ECS**: Orchestrating containerized Game Server applications using AWS Fargate.

- **Application Load Balancer (ALB)**: Providing a public entry point and distributing incoming WebSocket connections across Game Server containers.

- **Amazon ElastiCache for Redis**: Providing a low-latency in-memory data layer for sharing game session and real-time state information.

- **Amazon CloudWatch**: Collecting application and infrastructure metrics and managing centralized container logs.

#### Workshop Objectives

By completing this workshop, you will learn how to:

1. Design a secure and scalable AWS network architecture.

2. Configure IAM and authentication mechanisms for AWS resources.

3. Deploy a containerized WebSocket Game Server using Amazon ECS and AWS Fargate.

4. Configure Redis as an in-memory data layer for real-time applications.

5. Expose the Game Server through an Application Load Balancer.

6. Configure automatic scaling based on application resource utilization.

7. Monitor application performance and container logs using Amazon CloudWatch.

8. Perform load testing to evaluate the Game Server under high-concurrency workloads.

#### Workshop Implementation Navigation

1. [5.1. IAM & Regional Configuration](5.1-IAM%20%26%20Region%20Setup/)

2. [5.2. Networking](5.2-Networking/)

3. [5.3. Container](5.3-Container-Registry/)

4. [5.4. Database](5.4-Database/)

5. [5.5. Game Server](5.5-Game%20Server/)

6. [5.6. Load Balancing](5.6-Load-Balancing/)

7. [5.7. Scaling](5.7-Scaling/)

8. [5.8. Monitoring](5.8-Monitoring/)

9. [5.9. CI/CD](5.9-ci-cd/)

10. [5.10. Load Testing](5.10-load-testing/)