---
title: "Deploy Application"
date: "2025-10-27"
weight: 4
chapter: false
pre: " <b> 5.4 </b> "
---

# Deploy Application

Now that our infrastructure is ready (Network, Database, IAM), we can proceed to deploy the application components.

We will split this into two parts:
1.  **Backend Deployment**: Containerizing the Spring Boot app, pushing to ECR, and running securely on AWS Lambda with API Gateway.
2.  **Frontend Deployment**: Hosting the React SPA on S3 and distributing it globally via CloudFront.

Let's start with the Backend.
