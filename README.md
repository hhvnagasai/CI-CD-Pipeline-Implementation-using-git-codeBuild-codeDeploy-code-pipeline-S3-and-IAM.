# AWS CI/CD Pipeline for Node.js Application Deployment

## Project Overview

This project demonstrates a complete end-to-end CI/CD pipeline implementation on AWS for deploying a Node.js application into an EC2 instance using fully managed AWS DevOps services.

The pipeline automates:

- Source code integration from GitHub
- Continuous Integration using AWS CodeBuild
- Artifact management using Amazon S3
- Automated deployments using AWS CodeDeploy
- Deployment orchestration using AWS CodePipeline
- Secure access management using IAM Roles

This project follows real-world DevOps practices used in enterprise environments and production-grade CI/CD workflows.

---

# Architecture

```text
Developer
   |
   v
GitHub Repository
   |
   v
AWS CodePipeline
   |
   +----------------------+
   |                      |
   v                      v
Source Stage          Amazon S3
   |                  (Artifacts)
   v                      |
AWS CodeBuild             |
   |                      |
   v                      |
Build Artifact -----------+
   |
   v
AWS CodeDeploy
   |
   v
EC2 Instance
(CodeDeploy Agent)
   |
   v
Node.js Application
```

---

# AWS Services Used

| Service | Purpose |
|---|---|
| Amazon EC2 | Application hosting server |
| AWS CodePipeline | CI/CD workflow orchestration |
| AWS CodeBuild | Application build automation |
| AWS CodeDeploy | Automated EC2 deployment |
| Amazon S3 | Artifact storage |
| AWS IAM | Secure role-based access |
| GitHub | Source code repository |
| CloudWatch Logs | Build and deployment logging |

---

# Features Implemented

- Automated CI/CD pipeline
- GitHub integration with AWS
- Automated build and deployment workflow
- Node.js application deployment
- Artifact versioning through Amazon S3
- IAM role-based secure architecture
- CodeDeploy lifecycle hooks
- Deployment automation using appspec.yml
- Build automation using buildspec.yml
- EC2 deployment using CodeDeploy Agent
- Infrastructure aligned with industry DevOps practices

---

# Project Structure

```text
node-cicd-app/
│
├── app.js
├── package.json
├── buildspec.yml
├── appspec.yml
│
├── scripts/
│   ├── install_dependencies.sh
│   ├── start_server.sh
│   └── stop_server.sh
│
└── README.md
```

---

# CI/CD Workflow

## 1. Source Stage

- Developer pushes code into GitHub repository
- CodePipeline detects changes automatically
- Source artifact generated and stored in S3

---

## 2. Build Stage

AWS CodeBuild:
- Creates temporary build container
- Downloads source artifact
- Executes buildspec.yml
- Installs dependencies
- Generates deployment artifact
- Uploads build artifact to S3

---

## 3. Deployment Stage

AWS CodeDeploy:
- Identifies EC2 instance using deployment group tags
- CodeDeploy Agent downloads artifact from S3
- Executes appspec.yml lifecycle hooks
- Deploys Node.js application into EC2

---

# IAM Roles Used

## EC2-CodeDeploy-Role

Permissions:
- AmazonEC2RoleforAWSCodeDeploy
- AmazonS3ReadOnlyAccess

Purpose:
- Allows EC2 instance to communicate securely with AWS services

---

## CodeBuild-Service-Role

Permissions:
- AWSCodeBuildDeveloperAccess
- AmazonS3FullAccess

Purpose:
- Allows CodeBuild to access artifacts and logs

---

## CodeDeploy-Service-Role

Permissions:
- AWSCodeDeployRole

Purpose:
- Allows CodeDeploy to manage deployments

---

# Deployment Lifecycle Hooks

The deployment lifecycle is managed using appspec.yml.

## Hooks Used

| Hook | Purpose |
|---|---|
| ApplicationStop | Stops old Node.js process |
| AfterInstall | Installs npm dependencies |
| ApplicationStart | Starts Node.js application |

---

# Buildspec Configuration

The build process is managed using:

```yaml
version: 0.2

phases:
  install:
    runtime-versions:
      nodejs: 18

    commands:
      - npm install

  build:
    commands:
      - echo "Build started"

artifacts:
  files:
    - '**/*'
```

---

# AppSpec Configuration

```yaml
version: 0.0
os: linux

files:
  - source: /
    destination: /home/ec2-user/nodeapp

hooks:
  ApplicationStop:
    - location: scripts/stop_server.sh
      timeout: 300
      runas: ec2-user

  AfterInstall:
    - location: scripts/install_dependencies.sh
      timeout: 300
      runas: ec2-user

  ApplicationStart:
    - location: scripts/start_server.sh
      timeout: 300
      runas: ec2-user
```

---

# Security Best Practices Implemented

- IAM role-based authentication
- No hardcoded AWS credentials
- S3 bucket public access blocked
- Artifact encryption enabled
- Principle of least privilege
- Secure EC2 SSH access using PEM key authentication

---

# Monitoring and Troubleshooting

## CodeBuild Logs

Available in:
- Amazon CloudWatch Logs

---

## CodeDeploy Logs

Inside EC2:

```bash
/var/log/aws/codedeploy-agent/codedeploy-agent.log
```

---

# Deployment Verification

Access deployed application:

```text
http://<EC2-PUBLIC-IP>:3000
```

---

# Key DevOps Concepts Demonstrated

- Continuous Integration (CI)
- Continuous Deployment (CD)
- Infrastructure Automation
- Artifact Management
- Deployment Lifecycle Management
- IAM Security Architecture
- AWS Managed DevOps Services
- GitOps Workflow
- Deployment Automation
- EC2 Deployment Orchestration

---

# Real-World Production Concepts Covered

- Source-to-deployment automation
- Build isolation using temporary containers
- Agent-based deployment architecture
- Artifact-driven CI/CD workflow
- Lifecycle hook execution
- Secure service-to-service communication
- Deployment group targeting using EC2 tags

---

# Future Enhancements

- Blue/Green Deployments
- Docker Integration
- ECS/EKS Deployments
- Terraform Infrastructure as Code
- SonarQube Code Analysis
- Trivy Security Scanning
- Auto Scaling Group Integration
- Application Load Balancer Integration
- Monitoring using CloudWatch Alarms
- Slack/Email Notifications

---

# Skills Demonstrated

- AWS DevOps
- CI/CD Pipeline Engineering
- Linux Administration
- Git & GitHub
- AWS IAM
- EC2 Management
- Node.js Deployment
- AWS CodePipeline
- AWS CodeBuild
- AWS CodeDeploy
- Amazon S3
- Cloud Infrastructure Automation

---

# Author

Name: P.HARIHARA VENKATA NAGASAI

Role: DevOps Engineer / Cloud Engineer

---

# Conclusion

This project demonstrates the implementation of a production-style CI/CD pipeline using AWS managed DevOps services for automated Node.js application deployment.

The architecture follows modern DevOps practices focused on:
- automation
- scalability
- security
- deployment consistency
- operational reliability
