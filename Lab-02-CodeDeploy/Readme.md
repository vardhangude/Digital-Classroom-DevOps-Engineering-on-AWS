# 🚀 Lab 02 - Deploy an Application to an EC2 Fleet Using AWS CodeDeploy

## 📖 Overview

In this lab, I learned how to automate application deployments across multiple Amazon EC2 instances using **AWS CodeDeploy**.

Instead of manually copying application files to each server, AWS CodeDeploy was used to package, distribute, deploy, and manage application updates automatically. The deployment process included creating a deployment application, deployment group, packaging the application, storing artifacts in Amazon S3, monitoring deployments, and performing application updates.

---

## 🎯 Objectives

After completing this lab, I was able to:

- Deploy applications to multiple EC2 instances simultaneously
- Verify that the CodeDeploy Agent is installed and running
- Create a CodeDeploy Application
- Create a Deployment Group
- Package and upload deployment artifacts to Amazon S3
- Deploy applications using AWS CLI
- Monitor deployment status
- Redeploy updated application versions

---

## ☁️ AWS Services Used

- AWS CodeDeploy
- Amazon EC2
- Amazon S3
- AWS IAM
- AWS Systems Manager (Session Manager)
- AWS CLI

---

## 🏗 Architecture

```
Developer
      │
      ▼
Application Bundle
      │
      ▼
Amazon S3
      │
      ▼
AWS CodeDeploy
      │
      ▼
Deployment Group
      │
      ▼
EC2 Instance 1      EC2 Instance 2
      │                    │
      └────────Deploy──────┘
```

---

## 🛠 Implementation Steps

### Step 1

Reviewed the existing environment.

- Verified two EC2 instances were running
- Confirmed status checks passed
- Verified CodeDeploy Agent was installed

---

### Step 2

Created a CodeDeploy Application.

Application Name

```
HeartBeatProduction-App
```

Compute Platform

```
EC2 / On-Premises
```

---

### Step 3

Created a Deployment Group.

Configuration included:

- Service Role
- EC2 Instance Targets
- Instance Tags
- In-place Deployment
- AllAtOnce Deployment Strategy

---

### Step 4

Reviewed the application package.

The deployment package included:

- Application binaries
- PowerShell deployment scripts
- `appspec.yml`

---

### Step 5

Created an Amazon S3 bucket to store deployment artifacts.

Example command:

```bash
aws s3 mb s3://heartbeat-codedeploy-artifacts-<unique-name>
```

---

### Step 6

Uploaded the application bundle.

```bash
aws deploy push \
--application-name HeartBeatProduction-App \
--source HeartBeat-App \
--s3-location s3://<bucket-name>/HeartBeat-App.zip
```

---

### Step 7

Created a deployment.

```bash
aws deploy create-deployment \
--application-name HeartBeatProduction-App \
--deployment-group-name HeartBeatProduction-App-Group \
--deployment-config-name CodeDeployDefault.AllAtOnce
```

---

### Step 8

Monitored deployment progress using:

- AWS CodeDeploy Console
- Deployment Events
- Deployment Targets

---

### Step 9

Verified deployment.

Checked:

- HeartBeat Windows Service
- Service Logs
- Deployment Success

---

### Step 10

Redeployed an updated application version.

Repeated:

- Push new revision
- Create Deployment
- Verify updated service logs

---

## 📂 Application Bundle

The deployment package consisted of:

```
Heartbeat-App/
│
├── appspec.yml
├── Heartbeat.dll
├── HeartbeatService.exe
├── Logger.dll
├── log4net.dll
├── install.ps1
├── uninstall.ps1
└── copywintail.ps1
```

---

## 📄 appspec.yml

The **appspec.yml** file controls how CodeDeploy deploys the application.

Responsibilities include:

- File copy locations
- Lifecycle hooks
- Installation scripts
- Service start/stop operations

Example lifecycle hooks:

- ApplicationStop
- AfterInstall

---

## 🔄 Deployment Workflow

```
Developer
      │
      ▼
Application Bundle
      │
      ▼
Amazon S3
      │
      ▼
AWS CodeDeploy
      │
      ▼
Deployment Group
      │
      ▼
EC2 Fleet
      │
      ▼
Application Installed
```

---

## 💻 AWS CLI Commands Used

### Create S3 Bucket

```bash
aws s3 mb s3://bucket-name
```

### Push Deployment Package

```bash
aws deploy push
```

### Create Deployment

```bash
aws deploy create-deployment
```

---

## 📚 Key Learnings

- AWS CodeDeploy automates software deployment.
- Deployment Groups define deployment targets.
- Amazon S3 stores deployment artifacts.
- The CodeDeploy Agent performs deployments on EC2 instances.
- `appspec.yml` controls deployment behavior.
- Lifecycle hooks automate installation, stopping, and starting services.
- Deployments can be monitored in real time through the CodeDeploy Console.

---

## 🧠 Skills Gained

- AWS CodeDeploy
- Deployment Automation
- Amazon EC2
- Amazon S3
- AWS CLI
- Windows Service Deployment
- Infrastructure Automation
- CI/CD Fundamentals

---

## 📸 Screenshots

> *(Add your screenshots here after completing the lab.)*

- EC2 Instances
- CodeDeploy Application
- Deployment Group
- Deployment Success
- Deployment Events
- Running HeartBeat Service
- Application Logs

---

## ✅ Outcome

Successfully deployed and updated a sample application across multiple Amazon EC2 instances using AWS CodeDeploy while monitoring deployment progress and verifying successful application execution.
