# 🚀 Lab 04 - Deploying a Serverless Application Using AWS SAM and CI/CD Pipeline

## 📖 Overview

In this lab, I built, tested, and deployed a **serverless application** using the **AWS Serverless Application Model (AWS SAM)**. I then automated the deployment process by integrating **AWS CodeCommit**, **AWS CodeBuild**, **AWS CodePipeline**, **AWS CloudFormation**, and **AWS CodeDeploy**.

Finally, I implemented a **Blue/Green traffic shifting deployment**, enabling gradual rollout of application updates with minimal downtime and automatic rollback support.

---

## 🎯 Objectives

After completing this lab, I was able to:

- Build a serverless application using AWS SAM
- Test the application locally
- Package and deploy the application to AWS
- Configure an automated CI/CD pipeline
- Deploy AWS Lambda functions using CloudFormation
- Perform Blue/Green deployments with traffic shifting
- Automate deployments using Git commits

---

## ☁️ AWS Services Used

- AWS SAM
- AWS Lambda
- Amazon API Gateway
- AWS CloudFormation
- AWS CodeCommit
- AWS CodeBuild
- AWS CodePipeline
- AWS CodeDeploy
- Amazon S3
- AWS IAM

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
AWS CloudFormation
      │
      ▼
AWS Lambda + API Gateway
      │
      ▼
AWS CodeDeploy
      │
      ▼
Blue / Green Traffic Shifting
```

---

# 🛠 Implementation Steps

## Step 1

Connected to the AWS Code Editor IDE.

---

## Step 2

Initialized a new AWS SAM project.

```bash
sam init --runtime python3.13
```

---

## Step 3

Built the serverless application.

```bash
sam build
```

Output:

```
Build Succeeded
```

---

## Step 4

Tested the Lambda function locally.

```bash
sam local invoke HelloWorldFunction \
--event events/event.json
```

Response:

```json
{
  "statusCode": 200,
  "body": "{\"message\":\"hello world\"}"
}
```

---

## Step 5

Started the local API.

```bash
sam local start-api
```

Verified using:

```bash
curl http://127.0.0.1:8000/hello
```

Output:

```json
{
  "message":"hello world"
}
```

---

## Step 6

Created an Amazon S3 bucket for deployment artifacts.

```bash
aws s3 mb s3://<bucket-name>
```

---

## Step 7

Packaged the application.

```bash
sam package \
--output-template-file packaged.yaml \
--s3-bucket <bucket-name>
```

---

## Step 8

Deployed the serverless application.

```bash
sam deploy \
--template-file packaged.yaml \
--stack-name sam-app \
--capabilities CAPABILITY_IAM
```

CloudFormation created:

- Lambda Function
- IAM Role
- API Gateway
- CloudFormation Stack

---

## Step 9

Verified the deployed API.

Opened the API Gateway endpoint.

Expected response:

```json
{
  "message":"hello world"
}
```

---

## Step 10

Configured a CI/CD Pipeline.

Pipeline stages:

```
Source
↓

Build

↓

Deploy
```

Pipeline components:

- Source → AWS CodeCommit
- Build → AWS CodeBuild
- Deploy → AWS CloudFormation

---

## Step 11

Configured the Build Project.

Build specifications were defined using:

```
buildspec.yml
```

The build process packaged the SAM application and generated the CloudFormation template automatically.

---

## Step 12

Configured the Deployment Stage.

CloudFormation was configured to:

- Create a Change Set
- Execute the Change Set
- Deploy the updated application

---

## Step 13

Committed application changes.

```bash
git add .

git commit -m "Updated application"

git push
```

---

## Step 14

Automatic Deployment

After pushing code:

```
CodeCommit

↓

CodePipeline

↓

CodeBuild

↓

CloudFormation

↓

CodeDeploy

↓

Lambda
```

The deployment started automatically.

---

## Step 15

Blue/Green Deployment

AWS CodeDeploy gradually shifted traffic from the previous version to the updated version.

Traffic flow:

```
Old Version

100%

↓

70%

↓

50%

↓

30%

↓

0%

↓

New Version

100%
```

This ensured zero downtime during deployment.

---

## Step 16

Verified Deployment

Confirmed:

- Pipeline completed successfully
- CloudFormation stack updated
- Lambda function updated
- API Gateway served the new application
- Blue/Green deployment completed successfully

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

AWS CloudFormation

     │

     ▼

AWS CodeDeploy

     │

     ▼

AWS Lambda

     │

     ▼

Amazon API Gateway
```

---

# 💻 Commands Used

## Initialize SAM

```bash
sam init
```

---

## Build Application

```bash
sam build
```

---

## Local Invoke

```bash
sam local invoke
```

---

## Start Local API

```bash
sam local start-api
```

---

## Package Application

```bash
sam package
```

---

## Deploy Application

```bash
sam deploy
```

---

## Git Commands

```bash
git add .

git commit -m "Updated application"

git push
```

---

# 📚 Key Learnings

- AWS SAM simplifies serverless application development.
- SAM allows local testing before deployment.
- CloudFormation manages serverless infrastructure as code.
- CodePipeline automates the deployment process.
- CodeBuild packages the application automatically.
- CodeDeploy enables safe Blue/Green deployments.
- Traffic shifting minimizes downtime and deployment risks.
- Git commits automatically trigger deployments.

---

# 🧠 Skills Gained

- AWS SAM
- AWS Lambda
- API Gateway
- AWS CloudFormation
- AWS CodeCommit
- AWS CodeBuild
- AWS CodePipeline
- AWS CodeDeploy
- Blue/Green Deployments
- Traffic Shifting
- CI/CD
- Serverless Architecture

---

# 📸 Screenshots

- AWS SAM Build Success
- Local API Test
- API Gateway Output
- CloudFormation Stack
- CodeCommit Repository
- CodeBuild Project
- CodePipeline Success
- CloudFormation Change Set
- CodeDeploy Deployment
- Blue/Green Deployment Progress
- Updated Application Output

---

# ✅ Outcome

Successfully built, tested, and deployed a serverless application using **AWS SAM**. Automated the deployment process with **AWS CodeCommit**, **CodeBuild**, **CodePipeline**, **CloudFormation**, and **CodeDeploy**, while implementing **Blue/Green traffic shifting** to achieve safe, zero-downtime application releases.
