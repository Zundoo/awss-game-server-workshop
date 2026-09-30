---
title : "Week 4 Worklog"
date : "2026-08-17"
weight : 4
chapter : false
---

# Week 4 Worklog

### Week 4 Objectives:
* Learn Internet Gateway (IGW) connection mechanics.
* Learn Route Tables traffic filtering configuration.
* Learn stateful virtual firewall Security Groups deployment.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
|:---:|---|:---:|:---:|---|
| **1** | - Learn internet egress edge routing mechanisms.<br>- Review Internet Gateway attachment protocols.<br>- Map edge traffic routing pipelines. | 17/08/2026 | 17/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **2** | - Provision a system Internet Gateway instance.<br>- Attach the active IGW module to the custom VPC.<br>- Confirm ingress border gateway activation. | 18/08/2026 | 18/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **3** | - Learn Route Table management properties.<br>- Evaluate default routing vs custom tables.<br>- Study target destination network definitions. | 19/08/2026 | 19/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **4** | - Create custom external Route Tables.<br>- Add edge rules pointing `0.0.0.0/0` targets to the IGW.<br>- Bind public subnets to external tables. | 20/08/2026 | 20/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **5** | - Learn Security Groups stateful firewall mechanics.<br>- Review inbound ingress and outbound egress rule paradigms.<br>- Compare security groups with network ACL lists. | 21/08/2026 | 21/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **6** | - Provision specialized security firewalls.<br>- Configure `alb-sg` exposing standard port 80/443 lanes.<br>- Build `game-server-sg` isolating app port 8080. | 22/08/2026 | 22/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |
| **7** | - Test structural boundary connections.<br>- Verify isolated backend subnets reject public packets.<br>- Finalize initial boundary connectivity maps. | 23/08/2026 | 23/08/2026 | [AWS Study Group - FCJ](https://awsstudygroup.com) |

### Week 4 Achievements:
* **Activated External Network Egress:** Enabled bidirectional public communication vectors by mounting redundant VPC Internet Gateways.
* **Orchestrated Custom Subnet Routing:** Channeled edge public traffic routes distinctly away from hidden backend infrastructure layers.
* **Reinforced Perimeter Access Guards:** Standardized least-privilege boundary shields across system resource endpoints.
