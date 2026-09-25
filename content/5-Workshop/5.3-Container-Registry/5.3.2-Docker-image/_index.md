---
title: "4.2.2. Docker Image"
weight: 422
---

# 4.2.2. Crafting the Dockerfile Configuration

The Game Server application is containerized utilizing a lightweight **Dockerfile** pattern optimized for minimal memory footprint and fast boot time:

```dockerfile
# Use a lightweight Node.js Alpine base image
FROM node:18-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy dependency files and install production dependencies
COPY package*.json ./
RUN npm install --only=production

# Copy the rest of the application source code
COPY . .

# Expose the application network port
EXPOSE 8080

# Define the default runtime execution command
CMD ["node", "server.js"]
```
