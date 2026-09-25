---
title: "4.9.2. WebSocket Test"
weight: 492
---

# 4.9.2. Persistent WebSocket High-Concurrency Stress Test

Executed **Artillery** load profiles from a local console targeting the public **ALB DNS hostname** to simulate a massive user spike: Bursting **1,000 virtual users** within 1 second, propagating **46.500 real-time WebSocket messages**.

```text
Summary report
errors.Unexpected server response: 504: ....... 140
vusers.created: ............................... 1000
vusers.failed: ................................ 70
websocket.messages_sent: ...................... 46500
websocket.send_rate: .......................... 1629/sec
Total time: 35 seconds
```

### 🔬 In-Depth Architectural Root-Cause Evaluation
1.  **Ingress Throughput**: The cluster architecture maintained highly efficient pipeline scaling, processing an aggregate exchange rate peak of **1,629 messages/second** (`websocket.send_rate`).
2.  **Deciphering 504 Error Anomalies**: Introducing 1,000 requests instantly created a localized resource constraint (Spike Traffic), exhausting the computing threads and flooding the connection pool. The ALB attempted connection handshakes but the container task timed out, generating **140 system infrastructure `504 Gateway Timeout` errors** and dropping `70` initial user sessions.
3.  **Auto Scaling Mitigations**: The connection bottleneck pushed CPU utilization past the 70% threshold, alerting CloudWatch to invoke scaling policies. As soon as replicate task containers passed health evaluations, the `vusers.failed` metrics **dropped to absolute 0**. The architecture stabilized, safeguarding the remaining 930 active user sessions.

![ALB Active Connections Monitoring telemetry spiking up during stress tests](/images/4.9.2-websocket-test.png)
