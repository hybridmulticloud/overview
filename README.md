# 🌐 HybridMultiCloud · Cloud Resume Challenge

Welcome to the `hybridmulticloud` GitHub organization!

This project showcases a **modern cloud-native personal resume site** powered by serverless infrastructure, Infrastructure as Code (IaC), and CI/CD pipelines via **GitHub Actions** — fully automated, zero local deployment needed.

🏠 **Live Site**: [https://hybridmulti.cloud](https://hybridmulti.cloud)

---

## 🧩 Project Structure

| Repository | Description |
|------------|-------------|
| [`resume-api-frontend`](https://github.com/hybridmulticloud/resume-api-frontend) | Static resume website hosted via S3 + CloudFront |
| [`resume-api-backend`](https://github.com/hybridmulticloud/resume-api-backend) | Serverless backend for tracking visitor count (API Gateway + Lambda + DynamoDB) |

---

## 🔗 Interconnected Architecture

This project is split into two tightly-integrated components:

```plaintext
Visitor Browser
    │
    ▼
[CloudFront CDN]
    │
    ▼
[S3 Static Website]
    │   Embedded JS calls
    ▼
[API Gateway] ───> [Lambda Function] ───> [DynamoDB]
```

- The **frontend** dynamically fetches the visitor count from the **backend API**
- Backend artifacts (API Gateway URL & CloudFront Distribution ID) are exposed via GitHub Actions outputs
- These artifacts are picked up automatically by the frontend pipeline for content injection and cache invalidation

---

## ⚙️ GitHub Actions CI/CD

Both repositories use **GitHub Actions** to automate deployment:

- **Backend**
  - Terraform infrastructure setup (`infra.yml`)
  - Lambda deployment (`lambda-deploy.yml`)
  - Artifact output (`api-url`, `cloudfront-id`)

- **Frontend**
  - Uses backend artifacts
  - Injects URL into `index.tmpl.html`
  - Uploads static site to S3
  - Invalidates CloudFront cache

✅ No manual steps required. Deployments are fully Git-driven.

---

## 🧠 Why This Matters

This project demonstrates:
- Practical cloud skills (IAM, API Gateway, Lambda, S3, CloudFront, DynamoDB)
- Professional DevOps patterns (CI/CD pipelines, IaC, GitOps)
- Clear documentation and ownership — easy for teams or hiring managers to understand and extend

---

## 📚 Terraform Documentation

- [Backend Terraform Guide](terraform-backend.md)
- [Frontend Terraform Notes](terraform-frontend.md)

