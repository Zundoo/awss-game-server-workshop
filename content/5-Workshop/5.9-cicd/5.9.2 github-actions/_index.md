---
title: "4.8.2. GitHub Actions"
weight: 482
---

# 4.8.2. Constructing GitHub Actions Workflow Manifests

Create an automation runner script located at `.github/workflows/build-deploy.yml` to orchestrate automated AWS authentication, compile runtime artifacts, and push built packages to the private **Amazon ECR** registry on code commits.

```yaml
name: Game Server CI/CD Pipeline
on:
  push:
    branches: [ master ]
jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout Code
      uses: actions/checkout@v4
    - name: Configure AWS Credentials
      uses: aws-actions/configure-aws-credentials@v4
      with:
        aws-access-key-id: \${{ secrets.AWS_ACCESS_KEY_ID }}
        aws-secret-access-key: \${{ secrets.AWS_SECRET_ACCESS_KEY }}
        aws-region: ap-southeast-1
```
