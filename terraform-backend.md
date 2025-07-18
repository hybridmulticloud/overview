# 🛠️ Terraform Deployment · Backend

The backend uses **Terraform** to provision all necessary infrastructure:

## 📦 Resources Created

- S3 Bucket (for Lambda artifacts)
- IAM Role (for Lambda execution)
- Lambda Function (`UpdateVisitorCount`)
- DynamoDB Table (`VisitorCount`)
- API Gateway (HTTP API)

## 📂 File Structure

```
infra/
├── main.tf                # Root module and providers
├── data-sources.tf        # References to shared or remote resources
├── frontend_infra.tf      # Outputs required by frontend
├── variables.tf           # Input variables
├── lambda_stub.zip        # Empty stub to bootstrap the Lambda
```

## 🚀 Deployment Workflow

This is executed via GitHub Actions (`.github/workflows/infra.yml`):

1. `terraform init` to initialize the backend
2. `terraform plan` to preview changes
3. `terraform apply` to deploy infrastructure

Artifacts such as the API Gateway URL and CloudFront ID are passed to the frontend repo via GitHub Actions outputs.
