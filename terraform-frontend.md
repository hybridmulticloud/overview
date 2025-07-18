# 🛠️ Terraform Deployment · Frontend

The frontend itself is a static site hosted via **S3 + CloudFront**. Infrastructure is provisioned via the backend Terraform code, and frontend deploys only handle content.

## 💡 Note

Terraform does not directly provision the frontend infrastructure in this repo. Instead:

- The S3 bucket and CloudFront distribution are created by the backend Terraform stack
- The frontend CI/CD pipeline receives the `cloudfront_distribution_id` as an input
- GitHub Actions deploy the site content and handle cache invalidation

To update the static content, push changes to `main` and GitHub Actions will take care of it.
