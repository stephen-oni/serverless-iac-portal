# 🌌 CloudSphere: Automated Serverless Ecosystem
> **A high-performance, Infrastructure-as-Code (IaC) driven portal leveraging AWS Serverless architecture.**

---

![AWS](https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white)
![IaC](https://img.shields.io/badge/IaC-CloudFormation-FF9900?style=for-the-badge&logo=amazon-aws&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![Security](https://img.shields.io/badge/Security-IAM_Verified-blue?style=for-the-badge)

---

## 🎯 Executive Summary
CloudSphere is a sophisticated user-registration gateway designed to demonstrate the power of **Zero-Infrastructure** environments. By utilizing a **Serverless First** approach, this project achieves high availability with zero idle costs. The entire backend is defined through declarative **YAML templates**, ensuring rapid, error-free deployments.

---

## 🏗 System Architecture
The application follows a decoupled microservices pattern:

* **Presentation Layer:** A "Glassmorphism" UI optimized for modern browsers, utilizing CSS3 backdrop filters.
* **Entry Point:** **Amazon API Gateway** acting as a managed proxy for secure RESTful communication.
* **Compute Layer:** **AWS Lambda (Python)** handling business logic and input validation.
* **Persistence Layer:** **Amazon DynamoDB** providing a high-speed, NoSQL data store with on-demand scaling.

---

## 📜 Infrastructure as Code (IaC)
The project is built on the principle of **Repeatability**. The `templates/template.yaml` file automates the provisioning of all cloud resources.

### **Technical Highlights:**
> 🛡️ **IAM Least Privilege:** The Lambda function is restricted to `dynamodb:PutItem` permissions only, minimizing the security "blast radius."

> 💸 **On-Demand Scaling:** Configured with `PAY_PER_REQUEST` billing mode to ensure $0.00 cost when not in use.

```yaml
# Architectural Snippet: Secure DynamoDB Definition
UserTable:
  Type: AWS::DynamoDB::Table
  Properties:
    TableName: CloudSphere-Users
    BillingMode: PAY_PER_REQUEST
    AttributeDefinitions:
      - AttributeName: username
        AttributeType: S
    KeySchema:
      - AttributeName: username
        KeyType: HASH
