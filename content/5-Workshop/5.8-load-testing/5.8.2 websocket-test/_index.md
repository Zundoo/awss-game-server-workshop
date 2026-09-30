---
title : "Load Testing"
date : "`r Sys.Date()`"
weight : 6
chapter : false
pre : " <b> 5.2.6 </b> "
---

## Load Testing

This section guides you through executing load testing to evaluate the capacity, stability, and performance of the Game Server infrastructure under a massive volume of concurrent connections utilizing both WebSocket and HTTP protocols.

### 1. Test Objective

The primary goals of the load testing are to determine the system boundaries and its behavior under heavy stress, specifically:
* Validate Maximum Concurrency: Verify if the infrastructure successfully handles the target of 10,000+ simultaneous concurrent connections.
* Evaluate Latency: Ensure that response times for both WebSocket messages and HTTP APIs remain within an acceptable threshold of less than 200ms.
* Validate Auto Scaling: Confirm that ECS and EC2 auto-scaling policies trigger correctly when resource utilization spikes.
* Identify Bottlenecks: Detect any premature constraints related to hardware resources, network bandwidth, or application layer configurations.

### 2. Test Configuration

The open-source load testing tool Locust is configured with test scripts designed to simulate realistic player behavior:
* Tool Utilized: Locust.
* Simulated User Count: Gradually scaling up from 0 to 10,000 users at an acceleration ramp-up rate of 100 users per second.
* Behavioral Scenario: Initialize an HTTP handshake connection, upgrade to WebSocket via the ALB, transmit periodic ping-pong heartbeats every 5 seconds, and simulate continuous in-game actions at a frequency of 2 packets per second.

### 3. Test Architecture

To prevent the load generator itself from becoming a bottleneck due to local resource limits, a distributed load testing architecture is deployed:
* Locust Master: 1 EC2 instance positioned within the Public Subnet to coordinate test execution and serve the management dashboard.
* Locust Workers: Multiple EC2 instances deployed across subnets acting as load generators that directly simulate client traffic to the Application Load Balancer.
* Target System: All generated traffic is distributed through the ALB down to the Game Server cluster hosted inside the Private Subnet, which connects to ElastiCache Redis and the RDS Database.

![Distributed Load Testing Architecture Diagram](/images/5/5.2/load-test-architecture.png?featherlight=false&width=90pc)

### 4. Test Execution

The load testing workflow is conducted through the following operational steps:
1. Initialize the testing infrastructure, including both Locust Master and Worker instances, via the deployment configuration.
2. Access the Locust Master web interface via port 8089 on a web browser.
3. Configure the total simulated user target and the ramp-up spawn rate, pointing the target host URL to the ALB DNS name.

![Locust Web UI Parameter Setup Initialization](/images/5/5.2/locust-setup-ui.png?featherlight=false&width=80pc)

4. Launch the testing sequence and actively monitor the real-time growth curve of concurrent online users.
5. Sustain the peak load over a specific duration to verify the long-term stability and resilience of the system.

### 5. Test Results

The consolidated metric summary derived from the final load test report highlights the core performance indicators:

| Metric | Achieved Value | Status |
|---|---|---|
| Max Concurrent Users | 10,250 users | PASSED |
| Total Requests per Second | ~20,500 RPS | PASSED |
| Average Response Time | 42 ms | EXCELLENT |
| 95th Percentile Latency | 110 ms | PASSED |
| Error Rate | 0.02% | SAFE |

![Locust Dashboard Total Requests and Concurrent Users Analytics Chart](/images/5/5.2/locust-charts-results.png?featherlight=false&width=90pc)

### 6. CloudWatch Monitoring

Throughout the entire execution phase, fundamental infrastructure metrics are captured via Amazon CloudWatch to analyze system behavior under stress:
* ALB Metrics: Active connection count elevates linearly and peaks symmetrically in accordance with the simulated user metrics.
* Game Server Metrics: CPU utilization spikes trigger the pre-defined auto-scaling rules, successfully spinning up additional resource capacity to handle the workload.
* Redis Metrics: Resource consumption patterns across the caching tier demonstrate stable and optimized growth within safe operating parameters.

![System Infrastructure Performance Monitoring via Amazon CloudWatch Dashboard](/images/5/5.2/cloudwatch-loadtest-dashboard.png?featherlight=false&width=90pc)

### 7. Performance Analysis

Analyzing the combined dataset from the Locust reports and the CloudWatch metrics reveals several key technical takeaways:
* Success Highlights: The auto-scaling architecture responds exactly as designed. When resource metrics cross the 70% threshold, additional instances are integrated, maintaining minimal latency overhead for connected clients.
* Identified Issues: The environment initially dropped a small fraction of network requests due to standard system constraints on maximum open file descriptors.
* Remediation: Adjusted the open file descriptor thresholds (`ulimit -n`) inside the bootstrap launch configurations of the game server instances.

### 8. Conclusion

The load testing sequence concluded successfully, demonstrating that the network and security infrastructure fully comply with production-ready benchmarks. The overall architecture guarantees highly stable, real-time message processing performance even under extreme traffic anomalies.
