---
title : "Docker Image"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.3.2 </b> "
---

## Crafting the Dockerfile Configuration

The Game Server application is containerized using a lightweight **Dockerfile** configuration designed to reduce the container memory footprint and improve application startup time.

Create a file named `Dockerfile` in the root directory of the Game Server project:

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