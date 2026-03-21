# 🚀 Serverless Cloud Portal
### *Automated AWS Infrastructure via Infrastructure as Code (IaC)*

## 📖 Overview
This project is a high-performance web portal that uses a serverless backend. Instead of manual setup, the entire environment—API Gateway, Lambda, and DynamoDB—is deployed automatically using **YAML**.

## 🛠 Tech Stack
- **IaC:** AWS CloudFormation (YAML)
- **Backend:** AWS Lambda (Python), API Gateway
- **Database:** Amazon DynamoDB
- **Frontend:** HTML5, CSS3 (Glassmorphism)

## 📜 Infrastructure as Code (The YAML)
The `templates/template.yaml` file defines the entire architecture. 
- **Provisioning:** Creates the database and API.
- **Security:** Uses **IAM Roles** (Least Privilege) so the Lambda only talks to the specific table it needs. No hardcoded keys were used.

## 🚀 How to Deploy
1. Clone this repo.
2. Run the AWS CLI command:
   ```bash
   aws cloudformation deploy --template-file templates/template.yaml --stack-name my-stack --capabilities CAPABILITY_IAM