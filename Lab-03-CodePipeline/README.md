# 🚀 Lab 03 - Automating Code Deployments Using AWS CodePipeline

## 📖 Overview

In this lab, I automated application deployments by integrating **AWS CodePipeline** with **AWS CodeDeploy**.

Instead of manually deploying applications using the AWS CLI or CodeDeploy console, I built a CI/CD pipeline that automatically detects new application packages stored in Amazon S3 and deploys them to an Amazon EC2 fleet using AWS CodeDeploy.

This lab demonstrates the fundamentals of Continuous Integration and Continuous Delivery (CI/CD) on AWS.

---

## 🎯 Objectives

After completing this lab, I was able to:

- Configure AWS CodePipeline
- Integrate Amazon S3 as the source stage
- Integrate AWS CodeDeploy as the deployment stage
- Automate application deployments
- Monitor deployment progress
- Verify successful deployments using Systems Manager Session Manager
- Trigger automatic deployments by updating application artifacts

---

## ☁️ AWS Services Used

- AWS CodePipeline
- AWS CodeDeploy
- Amazon EC2
- Amazon S3
- AWS IAM
- AWS Systems Manager
- AWS CLI

---

# 🏗 Architecture

```
Developer
      │
      ▼
Application Package
      │
      ▼
Amazon S3 (Versioned Bucket)
      │
      ▼
AWS CodePipeline
      │
      ▼
AWS CodeDeploy
      │
      ▼
Deployment Group
      │
      ▼
EC2 Instance Fleet
```

---

# 🛠 Implementation Steps

## Step 1

Reviewed the existing environment.

Verified:

- CodeDeploy Application
- Deployment Group
- EC2 Fleet
- CodeDeploy Agent

---

## Step 2

Connected to AWS Code Editor IDE.

Used the terminal to prepare deployment artifacts.

---

## Step 3

Downloaded the application package.

Application:

```
CodeDeployHeartbeatDemo.zip
```

---

## Step 4

Uploaded the application bundle to an Amazon S3 bucket with versioning enabled.

Example command:

```bash
aws s3 cp CodeDeployHeartbeatDemo.zip \
s3://<ApplicationSourceBucket>/HeartBeat-App.zip
```

---

## Step 5

Created an AWS CodePipeline.

Pipeline Configuration

Pipeline Name

```
HeartBeatPipeline
```

Stages

```
Source
    │
Amazon S3

↓

Deploy
    │
AWS CodeDeploy
```

---

## Step 6

Configured Source Stage

Provider

```
Amazon S3
```

Object

```
HeartBeat-App.zip
```

---

## Step 7

Skipped Build Stage

Reason:

The application package was already compiled.

---

## Step 8

Skipped Test Stage

Reason:

Testing was outside the scope of this lab.

---

## Step 9

Configured Deploy Stage

Deployment Provider

```
AWS CodeDeploy
```

Application

```
HeartBeatProduction-App
```

Deployment Group

```
HeartBeatProduction-App-Group
```

Deployment Strategy

```
CodeDeployDefault.AllAtOnce
```

---

## Step 10

Created the pipeline.

AWS CodePipeline automatically:

- Retrieved the application package
- Triggered AWS CodeDeploy
- Deployed the application to both EC2 instances

---

## Step 11

Verified deployment.

Confirmed:

- HeartBeat Windows Service
- Running Service Status
- Application Logs

---

## Step 12

Updated the application.

Uploaded a new version of

```
HeartBeat-App.zip
```

to Amazon S3.

The pipeline detected the change automatically and deployed the updated application without manual intervention.

---

# 🔄 CI/CD Workflow

```
Developer

      │

      ▼

Amazon S3
(Application Package)

      │

      ▼

AWS CodePipeline

      │

      ▼

AWS CodeDeploy

      │

      ▼

EC2 Fleet

      │

      ▼

Application Running
```

---

# 💻 AWS CLI Commands Used

## Upload Application

```bash
aws s3 cp CodeDeployHeartbeatDemo.zip \
s3://bucket-name/HeartBeat-App.zip
```

---

## List Buckets

```bash
aws s3api list-buckets
```

---

## Verify Region

```bash
curl http://169.254.169.254/latest/meta-data/placement/region
```

---

# 📚 Key Learnings

- CodePipeline automates application delivery.
- Amazon S3 acts as the source repository.
- Versioned S3 buckets enable deployment tracking.
- CodePipeline automatically detects new application packages.
- CodeDeploy performs deployments to EC2 instances.
- Session Manager simplifies deployment verification.
- CI/CD pipelines reduce manual effort and deployment errors.

---

# 🧠 Skills Gained

- AWS CodePipeline
- AWS CodeDeploy
- Amazon S3
- Amazon EC2
- AWS CLI
- CI/CD
- Deployment Automation
- Infrastructure Automation

---

# 📸 Screenshots

Add screenshots after completing the lab:

- EC2 Fleet
- CodeDeploy Application
- Deployment Group
- S3 Bucket
- CodePipeline Stages
- Successful Pipeline Execution
- Deployment History
- Running HeartBeat Service
- Updated HeartBeat Logs

---

# ✅ Outcome

Successfully automated software deployments by integrating Amazon S3, AWS CodePipeline, and AWS CodeDeploy to deploy application updates across multiple Amazon EC2 instances. The pipeline automatically detected new application packages and performed deployments without manual intervention.
