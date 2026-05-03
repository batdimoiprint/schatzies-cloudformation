# Schatzies Events - Infrastructure as Code (CloudFormation)

This repository contains the AWS CloudFormation templates for the Schatzies Events infrastructure. It defines a serverless, highly available, and secure environment for hosting both the frontend and the backend API.

## Architecture Overview

The infrastructure is designed using AWS best practices for security and scalability:

### 1. Frontend Hosting (S3 + CloudFront)
- **AWS S3:** A private bucket (`schatzies-events-deployments`) serves as the origin for all static assets (React/Vite build).
- **AWS CloudFront:** Acts as the Content Delivery Network (CDN) and SSL/TLS terminator.
- **Origin Access Control (OAC):** Ensures the S3 bucket remains private, allowing access only via CloudFront.
- **SPA Support:** Custom error responses handle client-side routing by redirecting 403/404 errors to `index.html`.

### 2. Backend API (API Gateway + Lambda)
- **AWS API Gateway (HTTP API):** Provides a performant and cost-effective entry point for the backend.
- **AWS Lambda:** Runs the Node.js backend logic in a serverless environment.
- **API Proxying:** CloudFront routes all `/api/*` traffic to API Gateway, allowing the frontend and backend to share the same domain and avoid CORS issues.

### 3. Database (DynamoDB)
- **AWS DynamoDB:** NoSQL database with Pay-Per-Request billing for cost efficiency.
  - `schatzies_main_table`: Core data storage.
  - `schatzies_dashboard_analytics_table`: Analytics and reporting data.

### 4. Security & Identity (IAM)
- **Least Privilege Roles:** Lambda execution roles are scoped strictly to the required S3 and DynamoDB resources.
- **Local Development User:** A dedicated IAM user for secure local access to cloud resources.
- **GitHub Actions User:** Scoped permissions for automated deployments.

---

## Getting Started

### Prerequisites
- AWS CLI installed and configured.
- An existing ACM Certificate ARN (must be in `us-east-1` for CloudFront).

### Deployment

```bash
aws cloudformation deploy \
  --template-file cloudformation.yaml \
  --stack-name schatzies-infrastructure-prod \
  --parameter-overrides \
    DomainName=yourdomain.com \
    CertificateArn=arn:aws:acm:us-east-1:123456789012:certificate/uuid \
  --capabilities CAPABILITY_NAMED_IAM
```

---

## Clean Up
To remove all resources created by a stack:
```bash
aws cloudformation delete-stack --stack-name <your-stack-name>
```
*Note: S3 buckets must be emptied manually before the stack can be fully deleted.*
