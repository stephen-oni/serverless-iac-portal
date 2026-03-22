# 🌌 A Serverless Portal
> **A fully automated, zero-infrastructure web application powered by AWS Serverless and parameterized Infrastructure-as-Code.**

---

![AWS](https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white)
![IaC](https://img.shields.io/badge/IaC-CloudFormation-FF9900?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Frontend](https://img.shields.io/badge/UI-Glassmorphism-00d2ff?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

---

**[🎥 Watch the System Demonstration](https://youtu.be/h6PLl9imHA4)**

---

## 🎯 Executive Summary
A sophisticated user-registration gateway designed to demonstrate the power of **Zero-Infrastructure** environments. By utilizing a **Serverless First** approach, this project achieves high availability with zero idle costs. The entire backend and frontend hosting infrastructure is defined through declarative, fully parameterized **YAML templates**.

---

## 🏗 System Architecture
The application follows a decoupled, microservices pattern divided into two main layers:

### **1. The Presentation Layer (Frontend)**
* Hosted directly on an **Amazon S3 Website Bucket**.
* Built using pure `index.html` and `style.css`.
* Features a modern, responsive **Glassmorphism** UI utilizing CSS3 backdrop filters and advanced gradient mapping.

### **2. The Compute & Persistence Layer (Backend)**
* **Entry Point:** **Amazon API Gateway** acts as a managed proxy for secure RESTful communication (CORS enabled).
* **Compute:** **AWS Lambda (Python 3.12)** handles business logic, input validation, and dynamic error handling.
* **Database:** **Amazon DynamoDB** provides a high-speed, NoSQL data store configured for on-demand scaling.

---

## 📜 Automation
The project is built on the principle of **Repeatability**. The `templates/template.yaml` file automates the provisioning of all cloud resources uisng IaC.

### **The Highlights:**
> 🛡️ **Strict Parameterization:** Resource names are dynamically injected via CLI parameters. S3 Bucket names are strictly validated using Regular Expressions (`^[a-z0-9-]+$`) directly in the YAML to prevent deployment failures.

> 🔒 **Idempotent Database Operations:** The Lambda function utilizes DynamoDB `ConditionExpressions` (`attribute_not_exists`) to prevent data overwrites and return contextual 400-level HTTP errors to the frontend.

> 💸 **Zero-Cost Scaling:** Configured with `PAY_PER_REQUEST` billing mode to ensure $0.00 cost when idle.

---
## 🛡 Security & Best Practices
* **IAM Least Privilege:** The Lambda function is restricted via a custom IAM policy to only allow `dynamodb:PutItem`.
* **Environment Variables:** No hardcoded database names exist in the Python logic; everything is mapped dynamically via `os.environ`.
* **Client-Side Security:** The S3 bucket is configured with public read access explicitly limited to `s3:GetObject`.

---
## 🚀 Deployment Guide
### **Prerequisites**
* AWS CLI configured.
* Python 3.12+ for local function testing.

### **1. Provision the Infrastructure**
Run this command to build the S3 Bucket, API Gateway, Lambda, and DynamoDB. Replace the bucket name with a globally unique value:
```bash
aws cloudformation deploy \
  --template-file templates/template.yaml \
  --stack-name CloudSphere-Prod \
  --capabilities CAPABILITY_IAM \
  --parameter-overrides MyWebsiteBucketName=your-unique-bucket-name
