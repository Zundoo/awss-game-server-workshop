---
title: "4.2.3. Push Image"
weight: 423
---

# 4.2.3. Pushing Docker Image to Amazon ECR

Execute the following sequential commands on your staging terminal to authenticate, tag, and ship the built image artifact to the AWS cloud:

```bash
# 1. Authenticate Docker CLI against the private ECR registry endpoint
aws ecr get-login-password --region ap-southeast-1 | docker login --username AWS --password-stdin ://amazonaws.com

# 2. Compile and package the application into a Docker Image
docker build -t game-server .

# 3. Apply target ECR registry repository routing tag
docker tag game-server:latest ://amazonaws.com/game-server:latest

# 4. Ship the finalized Docker Image artifact to the AWS cloud
docker push ://amazonaws.com/game-server:latest
```
