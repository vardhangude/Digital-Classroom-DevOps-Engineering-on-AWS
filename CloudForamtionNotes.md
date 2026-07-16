# ☁️ AWS CloudFormation - Quick Revision Notes

> Concise notes for quick interview preparation and hands-on lab revision.

---

# What is AWS CloudFormation?

AWS CloudFormation is an **Infrastructure as Code (IaC)** service that allows you to define, provision, and manage AWS infrastructure using templates.

Instead of manually creating AWS resources, you define them in a **YAML** or **JSON** template, and CloudFormation provisions everything automatically.

## Key Benefits

- Infrastructure as Code (IaC)
- Automated resource provisioning
- Consistent and repeatable deployments
- Dependency management between resources
- Easy updates and rollbacks
- Version-controlled infrastructure
- Cost-effective and scalable deployments

---

# How CloudFormation Works

```
CloudFormation Template
        │
        ▼
      Stack
        │
        ▼
Creates AWS Resources
```

A **Template** defines all AWS resources.

A **Stack** is a collection of AWS resources created and managed together from a template.

---

# Template Formats

CloudFormation supports two formats:

- YAML ✅ (Recommended)
- JSON

> **Note:** Only **YAML** supports comments (`#`). JSON does not.

---

# Basic Template Structure

```yaml
AWSTemplateFormatVersion:
Description:

Parameters:

Resources:

Outputs:
```

## Sections

| Section | Purpose |
|----------|---------|
| Description | Information about the template |
| Parameters | User inputs during stack creation |
| Resources | AWS resources to create *(Required)* |
| Outputs | Values returned after stack creation |

---

# What is a Stack?

A **Stack** is a collection of AWS resources created from a single CloudFormation template.

Examples of resources inside a stack:

- VPC
- EC2
- Subnet
- Security Group
- Internet Gateway
- Route Table
- Elastic IP

CloudFormation creates, updates, and deletes these resources together.

---

# What is Drift?

**Drift** occurs when AWS resources are modified **outside CloudFormation**.

Example:

CloudFormation Security Group

```
HTTP
Source = 1.1.1.1/32
```

Someone manually changes it in the AWS Console:

```
HTTP
Source = 0.0.0.0/0
```

The actual resource no longer matches the template.

This difference is called **Drift**.

---

# Drift Detection

CloudFormation compares:

```
Expected Configuration
        VS
Actual AWS Resource
```

If they differ, the resource is marked as **DRIFTED**.

---

# Drift Status

| Status | Meaning |
|---------|---------|
| DETECTION_IN_PROGRESS | Drift detection is running |
| DETECTION_COMPLETE | Drift detection completed successfully |
| DETECTION_FAILED | Drift detection failed for one or more resources |
| DRIFTED | Resource differs from the template |
| IN_SYNC | Resource matches the template |
| NOT_CHECKED | Drift detection has not been run |

---

# Modifying a CloudFormation Template

Templates can be modified using:

- AWS CloudFormation Designer
- VS Code / Cloud9
- Any text editor

Typical workflow:

```
Download Template
        │
Modify Template
        │
Create Change Set
        │
Review Changes
        │
Execute Change Set
```

---

# What is a Change Set?

A **Change Set** allows you to preview changes before updating a CloudFormation stack.

Instead of directly updating infrastructure, CloudFormation shows:

- Resources to be created
- Resources to be modified
- Resources to be deleted

This helps avoid unexpected changes.

---

# Create a Change Set

```bash
aws cloudformation create-change-set \
  --stack-name NetworkStack \
  --change-set-name SampleChangeSet \
  --use-previous-template \
  --parameters \
    ParameterKey="InstanceType",UsePreviousValue=true \
    ParameterKey="KeyPairName",UsePreviousValue=true \
    ParameterKey="Purpose",ParameterValue="production"
```

---

# CloudFormation Workflow

```
Write Template
      │
      ▼
Validate Template
      │
      ▼
Create Stack
      │
      ▼
Deploy Resources
      │
      ▼
Verify Stack
      │
      ▼
Detect Drift
      │
      ▼
Create Change Set
      │
      ▼
Execute Change Set
```

---

# Common AWS CLI Commands

## Create Stack

```bash
aws cloudformation create-stack \
--stack-name Lab1 \
--template-body file://lab1.yaml
```

---

## Describe Stack

```bash
aws cloudformation describe-stacks \
--stack-name Lab1
```

---

## Validate Template

```bash
aws cloudformation validate-template \
--template-body file://lab1.yaml
```

---

## Detect Drift

```bash
aws cloudformation detect-stack-drift \
--stack-name Lab1
```

---

## Describe Drift

```bash
aws cloudformation describe-stack-resource-drifts \
--stack-name Lab1
```

---

## Create Change Set

```bash
aws cloudformation create-change-set \
--stack-name Lab1 \
--change-set-name Lab1ChangeSet \
--template-body file://lab1-CS.yaml
```

---

# Interview Tips

✅ CloudFormation is an **Infrastructure as Code (IaC)** service.

✅ A **Template** defines AWS resources.

✅ A **Stack** is a collection of resources created from a template.

✅ **Resources** is the only mandatory section in a CloudFormation template.

✅ YAML is preferred because it supports comments.

✅ Drift occurs when resources are modified outside CloudFormation.

✅ Use **Change Sets** to preview infrastructure updates before applying them.

✅ Always validate templates before creating a stack.

---

# Quick Summary

- Infrastructure as Code (IaC)
- Templates → YAML / JSON
- Stack = Collection of AWS Resources
- Resources section is mandatory
- YAML supports comments
- Drift = Manual configuration change
- Change Set = Preview before update
- Validate → Create → Detect Drift → Update
