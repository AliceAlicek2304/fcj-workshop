---
title: "Deploy Frontend"
date: "2025-10-27"
weight: 2
chapter: false
pre: " <b> 5.4.2 </b> "
---

# Deploy Frontend (React + S3 + CloudFront)

## 1. Create S3 Buckets

We need two buckets: one for the frontend code and one for game assets.

### CLI
```bash
# Frontend Bucket
aws s3 mb s3://gametracker-frontend --region ap-southeast-2

# Assets Bucket
aws s3 mb s3://gametracker-assets --region ap-southeast-2
```

### AWS Console
1. **S3 Console** → **Create bucket**.
2. Create `gametracker-frontend` (disable public access if using CloudFront OAC).
3. Create `gametracker-assets` (configure CORS as needed).

---

## 2. Create CloudFront Distribution

This ensures fast delivery and HTTPS.

### AWS Console
1. **CloudFront Console** → **Create distribution**.
2. **Origin domain**: Select `gametracker-frontend.s3...`.
3. **Origin access**: Select **Origin access control settings (recommended)** -> Create control setting.
   - *Important*: You must update the S3 bucket policy to allow CloudFront access (copy the policy AWS provides after creation).
4. **Viewer protocol policy**: Redirect HTTP to HTTPS.
5. **Default root object**: `index.html`.
6. **Error pages**:
   - Create custom error response for **403** and **404** -> Path `/index.html` -> Status **200**.
   - This is crucial for SPA routing to work.
7. Click **Create**.

---

## 3. Build & Deploy React App

Update your React app's API URL to point to the API Gateway Invoke URL you obtained in the previous step.

```bash
# 1. Build
npm run build

# 2. Sync to S3
aws s3 sync build/ s3://gametracker-frontend

# 3. Invalidate Cache (Optional but recommended)
aws cloudfront create-invalidation --distribution-id <DISTRIBUTION_ID> --paths "/*"
```

Your GameTracker application is now live at the CloudFront Domain Name!
