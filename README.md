# 🚀 CI Template: Deploy to S3 + CloudFront

CI pipeline for **building and deploying static applications** to an **S3 bucket**, with **automatic CloudFront cache invalidation**.

## ✅ Features
- App build process
- Upload to S3 with `cache-control`
- Automatic CloudFront invalidation
- Multi-environment support

## 🔐 Requirements
- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `AWS_REGION`
- `S3_BUCKET_NAME`
- `CLOUDFRONT_DISTRIBUTION_ID`

Perfect for static site hosting with CDN delivery.
