
# 🌐 HybridMulti.Cloud - Resume API Project

**Live Site:** [https://hybridmulti.cloud](https://hybridmulti.cloud)

---

## 🎯 Project Overview

This project is a full-stack cloud-native resume viewer that exposes a serverless REST API to track profile views and hosts a static website frontend. It's built with AWS and managed using Infrastructure as Code (Terraform).

---

## 🧠 Key Technologies

| Component      | Stack                                                                 |
|----------------|-----------------------------------------------------------------------|
| Backend        | Python, AWS Lambda, API Gateway, DynamoDB, Terraform, GitHub Actions |
| Frontend       | HTML, CSS, JavaScript, AWS S3, CloudFront, GitHub Actions            |
| Infrastructure | Terraform, AWS IAM, S3, API Gateway, Lambda, DynamoDB                |
| Monitoring     | CloudWatch, GitHub Actions                                            |

---

## 📁 Repository Structure

### `resume-api-backend`
- `src/lambda_function.py`: core API logic (view counter)
- `infra/*.tf`: Terraform for Lambda, API Gateway, DynamoDB
- `.github/workflows/`: CI/CD pipelines

### `resume-api-frontend`
- `public/index.tmpl.html`: dynamic HTML with injected API URL
- `.github/workflows/`: deploy to S3 + invalidate CloudFront

---

## 🚀 How to Deploy

```bash
# Backend
cd resume-api-backend/infra
terraform init && terraform apply

# Frontend (manual)
cd resume-api-frontend/public
aws s3 sync . s3://<bucket-name> --delete
```

---

## 🔐 Environment Variables

In GitHub Actions or local:
- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `AWS_REGION`

---

## 🧪 CI/CD Summary

- Backend deploys via Terraform + Lambda ZIP upload
- Frontend pushes to S3 with CDN invalidation
- Cross-repo: API URL output → injected into frontend template

---


## 🗺️ High-Level Architecture

```mermaid
flowchart TD
  User[Browser] --> CF[CloudFront CDN]
  CF --> S3[Static Website (S3)]
  CF --> API[API Gateway]
  API --> Lambda[AWS Lambda]
  Lambda --> DB[DynamoDB]
```

---

## 🔁 Backend Infra CI/CD Workflow

```mermaid
flowchart TD
  A[Checkout] --> B[Configure AWS]
  B --> C[Setup Terraform]
  C --> D[Terraform Init]
  D --> E[Terraform Plan + Apply]
```

---

## 🔁 Lambda CI/CD Workflow

```mermaid
flowchart TD
  A[Checkout] --> B[Configure AWS]
  B --> C[Setup Python]
  C --> D[Package Lambda ZIP]
  D --> E[Upload to S3]
  E --> F[Terraform Apply]
```

---

## 🔁 Frontend CI/CD Workflow

```mermaid
flowchart TD
  A2[Checkout] --> B2[Inject API URL to Template]
  B2 --> C2[Render HTML]
  C2 --> D2[Sync to S3]
  D2 --> E2[Invalidate CloudFront]
  E2 --> F2[Smoke Tests]
```

---

## 🔄 Cross-Repository CI/CD

```mermaid
flowchart LR
  subgraph Backend
    B1[Push] --> B2[Terraform Apply]
    B2 --> B3[Output: API URL]
  end

  subgraph Frontend
    F1[Push] --> F2[Inject API URL]
    F2 --> F3[Deploy to S3]
  end

  B3 --> F2
```

---

## 🧱 Full Infrastructure Map

```mermaid
flowchart LR
  GH[GitHub Actions]

  subgraph CI_CD
    GH --> TF["Terraform (Infra)"]
    GH --> LD["Lambda Deploy"]
    GH --> FD["Frontend Deploy"]
    GH --> MD["Monitoring Deploy"]
  end

  subgraph AWS
    TF --> APIGW["API Gateway"]
    APIGW --> Lambda["Lambda"]
    Lambda --> DynamoDB["DynamoDB"]
    Lambda --> CW["CloudWatch"]
    LD --> Lambda
    MD --> CW
    FD --> S3["S3 Bucket"]
    S3 --> CF["CloudFront"]
    CF --> Route53["Route 53"]
    Route53 --> User["Users"]
  end
```

---

## 🙋‍♂️ Author & Contribution

This project was fully designed and implemented by Kerem Kirci, a Senior Technical Consultant focused on hybrid/multi-cloud automation. It showcases:

- Serverless API design with AWS Lambda
- Full Infrastructure as Code with Terraform
- CI/CD pipelines with GitHub Actions
- Frontend templating and static site delivery via CloudFront

[LinkedIn](https://linkedin.com/in/kerem-kirci) | [GitHub](https://github.com/hybridmulticloud)

---
