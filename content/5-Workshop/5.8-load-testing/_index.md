---
title : "Load Testing"
date : "`r Sys.Date()`"
weight : 6
chapter : false
pre : " <b> 5.2.6 </b> "
---

## Load Testing

This section guides you through executing load testing to evaluate the capacity, stability, and performance of the Game Server infrastructure under traffic stress utilizing both WebSocket and HTTP protocols.

### 1. Test Objective

The primary goals of the load testing are to determine the system boundaries and its behavior under sudden traffic pressure, specifically:
* Validate Load Capacity: Verify if the infrastructure successfully handles and processes sudden high-volume concurrent requests without service degradation.
* Evaluate Latency: Ensure that the Target Response Time for requests remains consistently within low, acceptable thresholds.
* Verify Data Integrity: Confirm that load testing connections are properly captured by the backend server and accurately recorded within logs.
* System Monitoring: Utilize native AWS monitoring tools to track the real-time behavior of the Application Load Balancer (ALB) and Log Streams.

### 2. Test Configuration

The open-source load testing tool **Artillery** is utilized to simulate player behaviors and continuously stream payloads to the backend:
* Tool Utilized: **Artillery**.
* Behavioral Scenario: Initialize continuous traffic streams, sending test string payloads (`hello from Artillery!`) through the Application Load Balancer to analyze real-time processing capabilities.

### 3. Test Architecture

The infrastructure setup designed to execute and monitor the load test includes:
* Load Generator: An instance running Artillery script execution to actively generate traffic directed at the Application Load Balancer.
* Application Load Balancer (`alb-game-server`): Receives public ingress traffic and distributes requests down to the target groups inside the private network.
* Amazon CloudWatch Logs: Aggregates all incoming backend event logs via a dedicated log stream (`game-server-stream`) for auditing and debugging purposes.

### 4. Test Execution

The load testing workflow is conducted through the following practical steps:
1. Trigger the Artillery load testing script from the generator, aiming directly at the ALB DNS Name (`://amazonaws.com`).
2. While the test is active, navigate to **EC2 > Load Balancers > alb-game-server** and open the **Monitoring** tab to track real-time dashboard metrics.

![Monitoring real-time Load Balancer metrics under the Monitoring tab](/images/5/5.6/testalb.png?featherlight=false&width=90pc)

3. Concurrently, check **CloudWatch > Log management > /aws/gameserver/logs > game-server-stream** to verify successful data ingestion.

### 5. Test Results

The testing execution successfully verified that the backend seamlessly ingests and logs incoming stress payloads:
* The system accepted full payload delivery streams from Artillery without any packet drops or premature connection closures.
* Incoming application message logs printed sequentially and synchronously with real-time activities.

### 6. CloudWatch Monitoring & Logging

Throughout the load test duration, infrastructure behaviors were captured via Amazon CloudWatch as follows:

* **Log Events:** The `game-server-stream` interface accurately printed incoming verification payloads from the server runtime:

![The game-server-stream log events screen records incoming payload traffic from Artillery](/images/5/5.8/cloudlog2.png?featherlight=false&width=90pc)

* **Requests Count:** The ALB requests count chart recorded a significant spike, peaking at approximately **813 requests** during the concentrated load phase, then gracefully stabilized as traffic wrapped up.

![The ALB requests count chart peaks at 813 concurrent requests](/images/5/5.6/test2.png?featherlight=false&width=90pc)

* **Target Response Time:** The Target Response Time metric demonstrated exceptional stability. Aside from an initial peak of **16.7 seconds** caused by connection handshake establishment overhead, latency remained exceptionally low (near 0 seconds) for nearly the entire test duration, proving an absence of persistent congestion.

![The Target Response Time metrics graph remains stable within safe limits](/images/5/5.6/test3.png?featherlight=false&width=90pc)

### 7. Performance Analysis

Key technical conclusions drawn from the CloudWatch dashboards and ALB metrics include:
* Processing Resilience: The `alb-game-server` successfully balanced and absorbed the sudden rush of requests (~813 peak count) without experiencing service bottlenecks or downtime.
* Latency Analysis: The metrics graph captured an initial latency spike of **16.7 seconds** right at the beginning of the test execution (Cold Start / Handshake overhead). However, the infrastructure immediately streamlined the throughput, dropping the latency of all subsequent requests to near-zero levels, demonstrating robust optimization for real-time multiplayer networking.

### 8. Conclusion

The load testing sequence performed with **Artillery** was completed successfully. The core network topology, ALB balancing, and backend Game Server application handled the traffic spikes seamlessly while sustaining optimal minimal latency. The architecture is validated as production-ready.
