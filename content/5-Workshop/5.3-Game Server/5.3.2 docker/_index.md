---
title : "Docker Installation"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.3.2 </b> "
---

## Docker Installation

**Objective:** Install Docker and Docker Compose on the EC2 instance to run the Game Server container.

### Step-by-Step Implementation

1. Update the system and install Docker:

```bash
sudo dnf update -y
sudo dnf install -y docker
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker ec2-user