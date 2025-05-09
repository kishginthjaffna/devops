---

## **1. Core AWS Services for DevOps**

### EC2 (Elastic Compute Cloud)

* Virtual servers in the cloud
* Can be used to host CI/CD tools, Jenkins, GitLab Runners, etc.
* Key Features: AMIs, Security Groups, Auto Scaling, Elastic IPs

### S3 (Simple Storage Service)

* Object storage for storing build artifacts, logs, backups
* Common use: store deployment packages for Lambda/CodeDeploy
* Versioning and lifecycle policies are critical for automation

### IAM (Identity and Access Management)

* Controls access to AWS resources
* Use roles over long-term credentials
* Apply principle of least privilege
* Integrate IAM with CI/CD roles (e.g., CodeBuild, EC2)

### VPC (Virtual Private Cloud)

* Isolated network for hosting services securely
* Includes Subnets, Route Tables, NAT Gateways, Security Groups
* DevOps use: secure deployment environments, internal services

### CloudWatch

* Monitoring and observability service
* Logs: collect logs from EC2, Lambda, etc.
* Metrics: monitor CPU, memory, custom metrics
* Alarms: trigger actions like notifications or scaling

---

## **2. DevOps Toolchain in AWS**

### CodeCommit

* Git-based source control system
* Alternative to GitHub/GitLab for AWS-native environments

### CodeBuild

* Continuous integration service that builds and tests code
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

### CodeDeploy

* Automates application deployments to EC2, Lambda, or ECS
* Supports in-place and blue/green deployments
* Requires `appspec.yml` to define deployment steps

### CodePipeline

* Automates the entire release process
* Integrates with CodeCommit, CodeBuild, CodeDeploy, S3, Lambda
* Pipeline stages: Source → Build → Test → Deploy

### Elastic Beanstalk

* PaaS to deploy applications without managing infrastructure
* Supports auto-scaling, monitoring, rollback

### CloudFormation

* Infrastructure as Code service using JSON/YAML
* Define full stack: EC2, S3, IAM, VPC, etc.

### Terraform (3rd-party tool)

* Popular IaC tool that works with AWS via providers
* Benefits: modular, reusable, state management

---

## **3. Containers & Orchestration**

### ECR (Elastic Container Registry)

* Docker container registry for storing images

### ECS (Elastic Container Service)

* Run and manage Docker containers
* Fargate: serverless compute for containers

### EKS (Elastic Kubernetes Service)

* Managed Kubernetes on AWS
* Use with IaC (Terraform, eksctl)

---

## **4. Serverless DevOps**

### AWS Lambda

* Run code without managing servers
* Use for automation, deployment hooks, cron jobs

### API Gateway

* Expose Lambda functions as REST APIs

### EventBridge

* Event-driven automation
* Example: Trigger Lambda when CodeBuild fails

---

## **5. Monitoring, Logging, and Tracing**

### CloudWatch Logs & Metrics

* Collect logs from EC2, Lambda, ECS
* Create custom metrics and dashboards

### CloudTrail

* Logs all API activity in your account
* Important for auditing and compliance

### AWS X-Ray

* Distributed tracing for microservices

---

## **6. Security & Governance**

### IAM Policies

* Use scoped permissions for services
* Avoid wildcard (\*) permissions

### Secrets Manager & SSM Parameter Store

* Store and rotate credentials, API keys

### AWS Config

* Monitors configuration changes
* Ensures compliance with policies

---

## **7. Automation & Scheduling**

### CloudWatch Events / EventBridge

* Automate builds, backups, cleanups

### Step Functions

* Orchestrate complex workflows (e.g., approval-based deployment)

---

## **8. Sample DevOps Architecture in AWS**

1. **CodeCommit**: Developer pushes code
2. **CodePipeline**: Orchestrates the workflow
3. **CodeBuild**: Runs build & test
4. **S3**: Stores artifacts
5. **CodeDeploy**: Deploys to EC2 or Lambda
6. **CloudWatch**: Monitors performance
7. **X-Ray**: Traces execution paths

---

## **9. Best Practices**

* Use Infrastructure as Code for repeatability
* Automate testing and deployments
* Secure credentials with IAM and Secrets Manager
* Use multi-account strategy for dev/staging/prod
* Set up monitoring, logging, and alerts early

---

## 📚 **Helpful AWS Documentation for DevOps**

### 🚀 Core AWS Services

* [EC2 Documentation](https://docs.aws.amazon.com/ec2/)
* [S3 Documentation](https://docs.aws.amazon.com/s3/)
* [IAM Documentation](https://docs.aws.amazon.com/iam/)
* [VPC Documentation](https://docs.aws.amazon.com/vpc/)
* [CloudWatch Documentation](https://docs.aws.amazon.com/cloudwatch/)

### 🛠️ DevOps Toolchain in AWS

* [AWS CodeCommit Docs](https://docs.aws.amazon.com/codecommit/)
* [AWS CodeBuild Docs](https://docs.aws.amazon.com/codebuild/)
* [AWS CodeDeploy Docs](https://docs.aws.amazon.com/codedeploy/)
* [AWS CodePipeline Docs](https://docs.aws.amazon.com/codepipeline/)
* [Elastic Beanstalk Docs](https://docs.aws.amazon.com/elasticbeanstalk/)
* [CloudFormation Docs](https://docs.aws.amazon.com/cloudformation/)
* [Terraform AWS Provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)

### 📦 Containers & Orchestration

* [Amazon ECR Docs](https://docs.aws.amazon.com/ecr/)
* [Amazon ECS Docs](https://docs.aws.amazon.com/ecs/)
* [Amazon EKS Docs](https://docs.aws.amazon.com/eks/)

### ⚡ Serverless

* [AWS Lambda Docs](https://docs.aws.amazon.com/lambda/)
* [API Gateway Docs](https://docs.aws.amazon.com/apigateway/)
* [Amazon EventBridge Docs](https://docs.aws.amazon.com/eventbridge/)

### 🛡️ Monitoring, Security & Governance

* [CloudWatch Docs](https://docs.aws.amazon.com/cloudwatch/)
* [AWS CloudTrail Docs](https://docs.aws.amazon.com/cloudtrail/)
* [AWS X-Ray Docs](https://docs.aws.amazon.com/xray/)
* [AWS Secrets Manager Docs](https://docs.aws.amazon.com/secretsmanager/)
* [AWS Config Docs](https://docs.aws.amazon.com/config/)

### 🤖 Automation

* [AWS Step Functions Docs](https://docs.aws.amazon.com/step-functions/)
* [Amazon EventBridge Scheduler](https://docs.aws.amazon.com/scheduler/)

---

### ❤️ Made with love by **Kishgi**