# 📘 AWS DevOps Essentials

A curated guide to mastering core AWS services and DevOps tools.

---

## 🚀 1. Core AWS Services for DevOps

### 🖥️ EC2 (Elastic Compute Cloud)

* Virtual servers in the cloud
* Host CI/CD tools like Jenkins, GitLab Runners
* Key Features: AMIs, Security Groups, Auto Scaling, Elastic IPs

### 🗃️ S3 (Simple Storage Service)

* Object storage for artifacts, logs, backups
* Store deployment packages for Lambda/CodeDeploy
* Use versioning & lifecycle policies for automation

### 🔐 IAM (Identity and Access Management)

* Control access to AWS resources
* Prefer IAM roles over long-term credentials
* Apply least privilege principle
* Use IAM roles with CI/CD (e.g., CodeBuild, EC2)

### 🌐 VPC (Virtual Private Cloud)

* Isolated network environment
* Components: Subnets, Route Tables, NAT Gateways, Security Groups
* Secure deployment environments

### 📊 CloudWatch

* Monitoring and observability
* Logs: EC2, Lambda, ECS, etc.
* Metrics: CPU, memory, custom metrics
* Alarms: auto-scaling, notifications

---

## 🔧 2. DevOps Toolchain in AWS

### 📁 CodeCommit

* Git-based source control system
* AWS-native alternative to GitHub/GitLab

### 🏗️ CodeBuild

* Continuous integration service
* Uses `buildspec.yml` to define build steps

```yaml
version: 0.2
phases:
  install:
    commands:
      - echo Installing...
  build:
    commands:
      - echo Building...
artifacts:
  files:
    - '**/*'
```

### 🚀 CodeDeploy

* Automates app deployments to EC2, Lambda, ECS
* Supports in-place and blue/green deployments
* Uses `appspec.yml` for deployment steps

### 🔁 CodePipeline

* Automates the release pipeline
* Integrates with CodeCommit, CodeBuild, CodeDeploy, S3, Lambda
* Stages: Source → Build → Test → Deploy

### 🌿 Elastic Beanstalk

* PaaS for deploying applications
* No need to manage infrastructure
* Supports auto-scaling, monitoring, rollback

### 🏗️ CloudFormation

* AWS-native Infrastructure as Code tool (JSON/YAML)
* Manage EC2, S3, IAM, VPC, etc.

### 🔨 Terraform (3rd-party)

* Modular Infrastructure as Code tool
* Works with AWS via providers
* Supports state management and reusable modules

---

## 📦 3. Containers & Orchestration

### 📤 ECR (Elastic Container Registry)

* Store Docker images securely

### 🐳 ECS (Elastic Container Service)

* Run and manage Docker containers
* Fargate: serverless compute for containers

### ☸️ EKS (Elastic Kubernetes Service)

* Managed Kubernetes platform on AWS
* Use with Terraform or `eksctl`

---

## ⚡ 4. Serverless DevOps

### 🧠 AWS Lambda

* Run code without servers
* Ideal for automation and event-driven tasks

### 🌐 API Gateway

* Expose Lambda as RESTful APIs

### 🔄 EventBridge

* Event-driven architecture
* Example: Trigger Lambda when CodeBuild fails

---

## 📈 5. Monitoring, Logging, and Tracing

### 📄 CloudWatch Logs & Metrics

* Collect logs from EC2, Lambda, ECS
* Build custom dashboards and alarms

### 🔍 CloudTrail

* Audit log of all API activities
* Essential for compliance and governance

### 🕸️ AWS X-Ray

* Trace and visualize app performance across services

---

## 🔐 6. Security & Governance

### 🧾 IAM Policies

* Follow least privilege principle
* Avoid wildcard (`*`) permissions

### 🔑 Secrets Manager & SSM Parameter Store

* Securely store credentials, API keys

### 🧭 AWS Config

* Monitor configuration changes
* Enforce compliance rules

---

## ⏰ 7. Automation & Scheduling

### 📅 CloudWatch Events / EventBridge

* Automate builds, cleanups, backups

### 🔁 Step Functions

* Orchestrate complex workflows (e.g., approval-based deployment)

---

## 🏗️ 8. Sample DevOps Architecture

1. **CodeCommit** – Push code
2. **CodePipeline** – Orchestrate workflow
3. **CodeBuild** – Build & test
4. **S3** – Store artifacts
5. **CodeDeploy** – Deploy to EC2/Lambda
6. **CloudWatch** – Monitor
7. **X-Ray** – Trace app flows

---

## ✅ 9. Best Practices

* Use **Infrastructure as Code** for consistency
* Automate tests & deployments
* Secure credentials using IAM & Secrets Manager
* Use **multi-account strategy** (Dev, Staging, Prod)
* Set up monitoring, logging, alerts early

---

## 📚 Helpful AWS Documentation

### 🚀 Core Services

* [EC2](https://docs.aws.amazon.com/ec2/)
* [S3](https://docs.aws.amazon.com/s3/)
* [IAM](https://docs.aws.amazon.com/iam/)
* [VPC](https://docs.aws.amazon.com/vpc/)
* [CloudWatch](https://docs.aws.amazon.com/cloudwatch/)

### 🛠️ DevOps Tools

* [CodeCommit](https://docs.aws.amazon.com/codecommit/)
* [CodeBuild](https://docs.aws.amazon.com/codebuild/)
* [CodeDeploy](https://docs.aws.amazon.com/codedeploy/)
* [CodePipeline](https://docs.aws.amazon.com/codepipeline/)
* [Elastic Beanstalk](https://docs.aws.amazon.com/elasticbeanstalk/)
* [CloudFormation](https://docs.aws.amazon.com/cloudformation/)
* [Terraform AWS Provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)

### 🐳 Containers

* [ECR](https://docs.aws.amazon.com/ecr/)
* [ECS](https://docs.aws.amazon.com/ecs/)
* [EKS](https://docs.aws.amazon.com/eks/)

### ⚡ Serverless

* [Lambda](https://docs.aws.amazon.com/lambda/)
* [API Gateway](https://docs.aws.amazon.com/apigateway/)
* [EventBridge](https://docs.aws.amazon.com/eventbridge/)

### 🔒 Monitoring & Security

* [CloudTrail](https://docs.aws.amazon.com/cloudtrail/)
* [X-Ray](https://docs.aws.amazon.com/xray/)
* [Secrets Manager](https://docs.aws.amazon.com/secretsmanager/)
* [AWS Config](https://docs.aws.amazon.com/config/)

### 🤖 Automation

* [Step Functions](https://docs.aws.amazon.com/step-functions/)
* [EventBridge Scheduler](https://docs.aws.amazon.com/scheduler/)

---

### ❤️ Made with love by **Kishgi**
