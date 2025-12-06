---
title: "Cleanup Resources"
date: "2025-10-27"
weight: 7
chapter: false
pre: " <b> 5.7 </b> "
---

# Cleanup Resources

**Important**: To avoid unexpected charges, you must delete all resources created during this workshop. Follow the steps below in the specified order.

## 1. Delete Application Resources

1.  **Frontend (S3 & CloudFront)**:
    -   **CloudFront**: Disable the distribution -> Wait for it to deploy (stop) -> Delete it.
    -   **S3 Buckets**: Empty `gametracker-frontend` and `gametracker-assets`, then delete them.

2.  **Backend (Lambda & API Gateway & ECR)**:
    -   **API Gateway**: Delete the `gametracker-api` API.
    -   **Lambda**: Delete the `gametracker-api` function.
    -   **ECR**: Delete the `gametracker-backend` repository.

## 2. Delete Database

1.  **RDS Instance**:
    -   Go to **Amazon RDS** > **Databases**.
    -   Select `gametracker-mssql`.
    -   Action > **Delete**.
    -   Uncheck **Create final snapshot** and confirm deletion.
2.  **DB Subnet Group**:
    -   Go to **Subnet groups** -> Delete `gametracker-db-subnet-group`.

## 3. Delete Network Resources

1.  **NAT Gateway** (Expensive!):
    -   Go to **VPC** > **NAT Gateways**.
    -   Delete `gametracker-nat`.
    -   Wait for it to be `Deleted`.
2.  **Elastic IP**:
    -   Go to **Elastic IPs** -> Release the allocated IP.
3.  **VPC Endpoint**:
    -   Go to **Endpoints** -> Delete `gametracker-s3-endpoint`.
4.  **VPC**:
    -   Go to **Your VPCs** -> Select `gametracker-vpc` -> Actions -> **Delete VPC**.
    -   This will automatically delete Subnets, Route Tables, Internet Gateway, and Security Groups associated with it.

## 4. Verify

Check your **Billing Dashboard** the next day to ensure no active resources remain.
