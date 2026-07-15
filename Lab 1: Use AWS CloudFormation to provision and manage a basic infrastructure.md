# 🚀 LAB 1 - AWS CloudFormation to Provision and Manage a Basic Infrastructure

## 📌 Project Overview

This project demonstrates how to provision and manage AWS infrastructure using **AWS CloudFormation**.

The infrastructure is defined in a YAML template and deployed as a CloudFormation Stack. The project also demonstrates **Infrastructure as Code (IaC)** best practices including stack creation, drift detection, and stack updates using Change Sets.

---

## 🏗️ Architecture

The CloudFormation template provisions the following infrastructure:

- Amazon VPC
- Internet Gateway
- Public Subnet
- Route Table
- Route
- Security Group
- Elastic IP
- Amazon EC2 Instance
- Network ACL
- Route Table Association
- Subnet Association

```
                    Internet
                        │
                Internet Gateway
                        │
                     Route Table
                        │
                  Public Subnet
                        │
                Security Group
                        │
                Amazon EC2 Instance
                        │
                 Apache Web Server
```

---

# AWS Services Used

- AWS CloudFormation
- Amazon EC2
- Amazon VPC
- Internet Gateway
- Route Tables
- Security Groups
- Elastic IP
- Network ACL
- AWS CLI

---

# Project Objectives

- Build infrastructure using Infrastructure as Code (IaC)
- Deploy AWS resources using CloudFormation
- Manage infrastructure through templates
- Detect configuration drift
- Update infrastructure safely using Change Sets

---

# Features

✅ Infrastructure as Code (YAML)

✅ Parameterized EC2 Instance Type

✅ Automatic VPC Creation

✅ Public Subnet Deployment

✅ Internet Connectivity

✅ Apache Web Server Deployment

✅ Security Group Configuration

✅ CloudFormation Outputs

✅ Drift Detection

✅ Change Set Deployment

---

# CloudFormation Template Sections

The template consists of the following sections:

- Description
- Parameters
- Resources
- Outputs

---

# Parameters

| Parameter | Description |
|------------|-------------|
| InstanceType | EC2 Instance Type |
| VPCCIDR | VPC CIDR Block |
| PUBSUBNET1 | Public Subnet CIDR |
| LatestAmiId | Latest Amazon Linux AMI |

---

# Resources Created

| Resource |
|----------|
| VPC |
| Internet Gateway |
| Public Subnet |
| Route Table |
| Route |
| Security Group |
| Elastic IP |
| EC2 Instance |
| Network ACL |
| Route Table Association |

---

# Deployment

## Create Stack

```bash
aws cloudformation create-stack \
--stack-name Lab1 \
--parameters ParameterKey=InstanceType,ParameterValue=t2.micro \
--template-body file://lab1.yaml
```

---

## Verify Stack Status

```bash
aws cloudformation describe-stacks \
--stack-name Lab1
```

Check Stack Status

```bash
aws cloudformation describe-stacks \
--stack-name Lab1 \
--query "Stacks[0].StackStatus"
```

---

# Drift Detection

One of the key CloudFormation features demonstrated in this project is **Drift Detection**.

## Scenario

The Security Group was manually modified outside CloudFormation.

Expected Rule

```
1.1.1.1/32
```

Modified Rule

```
0.0.0.0/0
```

CloudFormation successfully detected the configuration drift.

Command used:

```bash
aws cloudformation describe-stack-resource-drifts \
--stack-name Lab1 \
--stack-resource-drift-status-filters MODIFIED DELETED
```

---

# Updating Infrastructure using Change Sets

Instead of manually changing infrastructure, CloudFormation Change Sets were used.

Create Change Set

```bash
aws cloudformation create-change-set \
--stack-name Lab1 \
--change-set-name Lab1ChangeSet \
--parameters ParameterKey=InstanceType,ParameterValue=t2.micro \
--template-body file://lab1-CS.yaml
```

Execute Change Set from CloudFormation Console.

---

# Outputs

After successful deployment CloudFormation returns:

- EC2 Public IP
- Application URL

Example:

```
http://<Public-IP>
```

Opening the URL displays the Apache Web Server homepage.

---

# Project Workflow

```
Create YAML Template
        │
        ▼
Create CloudFormation Stack
        │
        ▼
Deploy Infrastructure
        │
        ▼
Verify Resources
        │
        ▼
Modify Security Group
        │
        ▼
Detect Drift
        │
        ▼
Create Change Set
        │
        ▼
Execute Change Set
        │
        ▼
Infrastructure Updated
```

---

# Skills Demonstrated

- Infrastructure as Code (IaC)
- AWS CloudFormation
- YAML
- AWS CLI
- Amazon EC2
- Amazon VPC
- Security Groups
- Route Tables
- CloudFormation Change Sets
- Drift Detection
- Cloud Infrastructure Automation

---

# Learning Outcomes

After completing this project, I gained practical experience in:

- Designing AWS infrastructure using CloudFormation
- Automating infrastructure deployment
- Managing AWS resources through Infrastructure as Code
- Detecting infrastructure drift
- Updating cloud resources using Change Sets
- Deploying and validating cloud environments using AWS CLI

---

# Repository Structure

```
AWS-CloudFormation-IaC/
│
├── README.md
├── lab1.yaml
├── lab1-CS.yaml
├── screenshots/
│   ├── stack-created.png
│   ├── drift-detection.png
│   ├── change-set.png
│   ├── app-running.png
│   └── architecture.png
```

---

# Future Improvements

- Add Auto Scaling Group
- Add Application Load Balancer
- Deploy using GitHub Actions
- Integrate with CodePipeline
- Add CloudWatch Monitoring
- Add SNS Notifications
- Modularize templates using Nested Stacks

---

# Author

**Vardhan Gude**

DevOps | Cloud Engineer

AWS • Terraform • Docker • Kubernetes • Jenkins • Linux • GitHub Actions

---

⭐ If you found this project helpful, consider giving it a Star.
