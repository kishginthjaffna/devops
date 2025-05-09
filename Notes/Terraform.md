# Terraform Notes for DevOps

## Problem Terraform Solves

Managing infrastructure manually is error-prone and inefficient. As applications scale, the infrastructure becomes more complex and difficult to track or standardize. Automating this process with code becomes crucial.

## Solution: Terraform

Terraform, developed by HashiCorp, is an open-source Infrastructure as Code (IaC) tool. It allows you to provision and manage cloud, on-prem, and SaaS infrastructure using a declarative configuration language.

### How Terraform Works

```
Terraform <--> Terraform Provider <--> Target API
```

* **Terraform Core**: Handles the execution plans, resource graphs, and state management.
* **Providers**: Interfaces to external platforms like AWS, Azure, GCP.

### Key Features

* Manage any kind of infrastructure
* Track infrastructure changes
* Automate provisioning
* Standardize environment configurations
* Enable team collaboration

---

## Installation

Install Terraform CLI: [https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)

---

## Basic Terraform Workflow

1. `terraform init`
2. `terraform plan`
3. `terraform apply`
4. `terraform destroy`

---

## Sample `main.tf` for AWS

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.16"
    }
  }
  required_version = ">= 1.2.0"
}

provider "aws" {
  region = "us-west-2"
}

resource "aws_instance" "app_server" {
  ami           = "ami-0c55b159cbfafe1f0" # Example AMI
  instance_type = "t2.micro"

  tags = {
    Name = "Terraform_Demo"
  }
}
```

### Explanation

* **terraform**: Specifies required providers and versions.
* **provider**: AWS region configuration.
* **resource**: Creates an EC2 instance.

---

## Adding Another AWS Resource - Load Balancer

```hcl
resource "aws_lb" "app_lb" {
  name               = "app-load-balancer"
  internal           = false
  load_balancer_type = "application"
  security_groups    = ["sg-0123456789abcdef0"]
  subnets            = ["subnet-abc", "subnet-def"]

  tags = {
    Name = "AppLB"
  }
}
```

### AWS Docs

* [https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/lb](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/lb)

---

## Supporting Files

### `input.tf`

Used to define variable inputs for the configuration.

```hcl
variable "region" {
  description = "AWS region"
  type        = string
  default     = "us-west-2"
}
```

### `variables.tf`

Holds all variable declarations.

```hcl
variable "instance_type" {
  description = "EC2 instance type"
  type        = string
  default     = "t2.micro"
}
```

### `output.tf`

Defines output values to display after execution.

```hcl
output "instance_id" {
  description = "The ID of the instance"
  value       = aws_instance.app_server.id
}
```

### `terraform.tfstate`

Tracks the current state of the infrastructure. **DO NOT SHARE** this file. Store it in remote backends like S3.

### Remote Backend Setup in `main.tf`

```hcl
terraform {
  backend "s3" {
    bucket         = "my-terraform-state-bucket"
    key            = "path/to/my/key"
    region         = "us-west-2"
    dynamodb_table = "terraform-lock-table"
    encrypt        = true
  }
}
```

---

## Image: Ideal Terraform Setup

![Terraform Setup](https://miro.medium.com/v2/0*VjyKowTVE_Md97uB.jpeg)

---

## Terraform Modules

Modules allow you to group and reuse resources.

### Example Module

**Directory structure:**

```
modules/
  ec2/
    main.tf
    variables.tf
    output.tf
```

**modules/ec2/main.tf**

```hcl
resource "aws_instance" "example" {
  ami           = var.ami
  instance_type = var.instance_type
}
```

**modules/ec2/variables.tf**

```hcl
variable "ami" {}
variable "instance_type" {}
```

**Root module usage:**

```hcl
module "ec2_instance" {
  source        = "./modules/ec2"
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}
```

---

## Problems with Terraform

* **Single State File**: If corrupted, it breaks everything.
* **Manual Changes**: Manual cloud changes aren’t reflected.
* **Not GitOps Friendly**: Doesn’t play well with tools like ArgoCD and Flux.

### What is GitOps?

GitOps is a methodology where Git is the single source of truth. Infrastructure and application configurations are stored in Git and automatically applied by CD tools.

### Tools

* **ArgoCD**: Declarative GitOps CD tool for Kubernetes.
* **Flux**: GitOps operator for continuous delivery on Kubernetes.

### Challenges

* Terraform doesn’t natively support GitOps flows well.
* Requires manual work to reconcile state changes.

---

## Terraform vs Ansible

* **Terraform**: Best for provisioning infrastructure (e.g., servers, networks).
* **Ansible**: Best for configuration management (e.g., installing software).

> Today, boundaries are blurring. Ansible supports provisioning, and Terraform supports some configuration.

---
