---
title: "4.9.1. HTTP Test"
weight: 491
---

# 4.9.1. Testing HTTP Health Check Endpoint Ingress

*   **Objective**: Measure the stability and response performance of the static `/health` API under continuous health check queries from the load balancer layer.
*   **Outcomes**: The HTTP route resolved consistently with an ultra-low mean Response Time under 5ms. The HTTP status code `200 OK` hit a 100% success ratio, verifying the efficiency of the health check implementation.
