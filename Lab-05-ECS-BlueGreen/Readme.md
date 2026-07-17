# 🚀 Lab 05 - Blue/Green Deployments with Amazon ECS, AWS Fargate, and CI/CD

## 📖 Overview

In this lab, I built a complete CI/CD pipeline for a containerized web application using **AWS CodePipeline**, **AWS CodeBuild**, **Amazon ECR**, **Amazon ECS**, **AWS Fargate**, and **AWS CodeDeploy**.

The pipeline automatically builds Docker images, stores them in Amazon ECR, deploys them to an ECS cluster, and performs **Blue/Green deployments** with zero downtime using AWS CodeDeploy.

---

## 🎯 Objectives

After completing this lab, I was able to:

- Build Docker container images
- Store container images in Amazon ECR
- Create a CI/CD pipeline using AWS CodePipeline
- Deploy containerized applications on Amazon ECS with AWS Fargate
- Configure Blue/Green deployments using AWS CodeDeploy
- Automate application deployments through Git commits
- Perform zero-downtime application updates

---

# ☁️ AWS Services Used

- Amazon ECS
- AWS Fargate
- Amazon ECR
- AWS CodeCommit
- AWS CodeBuild
- AWS CodePipeline
- AWS CodeDeploy
- Application Load Balancer (ALB)
- IAM

---

# 🏗 Architecture

```
Developer
      │
      ▼
AWS CodeCommit
      │
      ▼
AWS CodePipeline
      │
      ▼
AWS CodeBuild
      │
      ▼
Docker Image
      │
      ▼
Amazon ECR
      │
      ▼
AWS CodeDeploy
      │
      ▼
Amazon ECS (Fargate)
      │
      ▼
Application Load Balancer
      │
      ▼
Users
```

---

# 🛠 Implementation Steps

## Step 1

Connected to the AWS Code Editor IDE.

---

## Step 2

Configured the `buildspec.yml` file.

Updated:

- Amazon ECR Repository URI
- Docker image build configuration
- Image push commands

---

## Step 3

Committed the changes to AWS CodeCommit.

```bash
git add .

git commit -m "Updated buildspec file"

git push
```

---

## Step 4

Created a CI/CD pipeline.

Pipeline Name

```
my-webapp-pipeline
```

Pipeline stages:

```
Source

↓

Build
```

---

## Step 5

Configured the Source Stage.

Provider

```
AWS CodeCommit
```

Repository

```
my-webapp-repo
```

Branch

```
main
```

---

## Step 6

Configured AWS CodeBuild.

The build process:

- Builds Docker image
- Tags image
- Pushes image to Amazon ECR

---

## Step 7

Created an ECS Task Definition.

Configured:

- Task Definition
- Execution Role
- Container Definition
- Image URI
- CPU
- Memory
- Port Mapping

---

## Step 8

Updated the task definition.

Replaced the image URI with the placeholder:

```
<IMAGE1_NAME>
```

This allows CodePipeline to inject the latest image automatically during deployments.

---

## Step 9

Created an ECS Service.

Configuration included:

- ECS Cluster
- Fargate Launch Type
- Application Load Balancer
- Target Group
- Networking
- Security Group
- Desired Task Count

---

## Step 10

Committed ECS configuration files.

```bash
git add .

git commit -m "Updated task definition"

git push
```

---

## Step 11

Verified the application deployment.

Accessed the application through the Application Load Balancer.

Initial deployment:

```
Blue Environment
```

---

## Step 12

Created an AWS CodeDeploy Application.

Configuration:

```
Compute Platform

Amazon ECS
```

---

## Step 13

Created a Deployment Group.

Configured:

- ECS Cluster
- ECS Service
- Application Load Balancer
- Target Groups
- Traffic Routing

Deployment Strategy:

```
CodeDeployDefault.ECSAllAtOnce
```

---

## Step 14

Added the Deploy stage to CodePipeline.

Pipeline stages became:

```
Source

↓

Build

↓

Deploy
```

---

## Step 15

Configured Blue/Green Deployment.

Deployment artifacts included:

- appspec.yaml
- taskdef.json
- Docker Image
- Image Detail Artifact

---

## Step 16

Updated the application.

Modified the Dockerfile.

Changed:

```
background-color

Blue

↓

Green
```

Committed changes:

```bash
git add .

git commit -m "Updated Dockerfile"

git push
```

---

## Step 17

Automatic Deployment

The Git push automatically triggered:

```
CodeCommit

↓

CodePipeline

↓

CodeBuild

↓

Amazon ECR

↓

CodeDeploy

↓

Amazon ECS
```

---

## Step 18

Blue/Green Deployment

Deployment flow:

```
Blue Environment

↓

Green Environment Created

↓

Traffic Shifted

↓

Blue Environment Removed
```

Users experienced **zero downtime** during deployment.

---

## Step 19

Verified Deployment

Confirmed:

- Pipeline completed successfully
- Docker image built successfully
- Image stored in Amazon ECR
- ECS service updated
- Traffic shifted successfully
- Application background changed from Blue to Green

---

# 🔄 CI/CD Workflow

```
Developer

      │

      ▼

AWS CodeCommit

      │

      ▼

AWS CodePipeline

      │

      ▼

AWS CodeBuild

      │

      ▼

Docker Image

      │

      ▼

Amazon ECR

      │

      ▼

AWS CodeDeploy

      │

      ▼

Amazon ECS (Fargate)

      │

      ▼

Application Load Balancer

      │

      ▼

Users
```

---

# 💻 Commands Used

## Git

```bash
git add .

git commit -m "Updated buildspec"

git push
```

---

## ECS Task Registration

```bash
aws ecs register-task-definition \
--cli-input-json file://taskdef.json
```

---

## ECS Service Creation

```bash
aws ecs create-service \
--service-name MyApp-Web-service \
--cli-input-json file://create-service.json
```

---

# 📚 Key Learnings

- Amazon ECR stores versioned Docker images.
- CodeBuild automatically builds and pushes Docker images.
- ECS Task Definitions describe container configurations.
- ECS Services maintain the desired number of running tasks.
- AWS Fargate eliminates the need to manage EC2 instances.
- CodeDeploy performs Blue/Green deployments for ECS services.
- Application Load Balancer manages traffic switching.
- CodePipeline automates container delivery from source code to production.

---

# 🧠 Skills Gained

- Docker
- Amazon ECR
- Amazon ECS
- AWS Fargate
- AWS CodeCommit
- AWS CodeBuild
- AWS CodePipeline
- AWS CodeDeploy
- Blue/Green Deployment
- Container CI/CD
- Load Balancing
- DevOps Automation

---

# 📸 Screenshots

- CodeCommit Repository
- buildspec.yml
- CodeBuild Success
- Amazon ECR Repository
- ECS Cluster
- ECS Task Definition
- ECS Service
- CodeDeploy Application
- Deployment Group
- CodePipeline Success
- Blue Environment
- Green Environment
- Application Load Balancer
- Final Green Application

---

# ✅ Outcome

Successfully built an end-to-end containerized CI/CD pipeline using **AWS CodeCommit**, **CodeBuild**, **Amazon ECR**, **Amazon ECS (AWS Fargate)**, **CodePipeline**, and **AWS CodeDeploy**. Automated Docker image creation and deployment while implementing **Blue/Green deployments** to achieve zero-downtime application releases.
