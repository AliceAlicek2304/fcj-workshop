---
title: "Introduction"
date: "2025-10-27"
weight: 1
chapter: false
pre: " <b> 5.1 </b> "
---

# Deploy GameTracker on AWS

## 🎯 Workshop Objective
In this workshop, we will practice deploying **GameTracker**—a full-stack web application—to AWS completely from scratch. You will build a standard serverless architecture using industry-popular services.

The goal is to create a production-like environment in the **Sydney (ap-southeast-2)** region, covering everything from networking setup to application deployment.

## 🏗️ Architecture Overview

The solution adopts a modern cloud-native architecture:
- **Frontend**: React Single Page Application (SPA) hosted on **Amazon S3** and distributed via **Amazon CloudFront**.
- **Backend**: Spring Boot application containerized with Docker, stored in **Amazon ECR**, and running as serverless on **AWS Lambda**, exposed via **API Gateway**.
- **Database**: **SQL Server Express** running on **Amazon RDS** for managing structured game data.
- **Network**: A custom **VPC** with public/private subnets and security groups for isolation and security.

![Architecture](/images/2-Proposal/GameTracker1.jpg)

## 📋 Services Used
We will configure the following AWS services:

| Category | Service |
|----------|----------|
| **Networking** | VPC, Subnets, Internet Gateway, NAT Gateway (Optional), Route53 |
| **Compute** | AWS Lambda, API Gateway (HTTP API) |
| **Storage** | Amazon S3 (Frontend & Assets) |
| **Database** | Amazon RDS (SQL Server) |
| **Container** | Amazon ECR (Elastic Container Registry) |
| **CDN & Security** | Amazon CloudFront, AWS WAF, IAM, Security Groups |

## 🚀 Deployment Steps
This workshop is divided into logical stages:

1.  **Network Setup**: Create VPC, Subnets, and Routing.
2.  **Database Provisioning**: Set up RDS SQL Server.
3.  **Backend Deployment**:
    - Create ECR Repository.
    - Build and push Docker image.
    - Create Lambda function and connect to the database.
    - Expose backend via API Gateway.
4.  **Frontend Deployment**:
    - Create S3 buckets.
    - Set up CloudFront distribution.
    - Deploy React application.
5.  **Cleanup**: Instructions to remove resources to avoid costs.

## 🛠️ Prerequisites

Before starting, ensuring you have the following:

1.  **AWS Account**: Active account with admin permissions.
2.  **Tools Installed**:
    -   [AWS CLI](https://aws.amazon.com/cli/) (Configured with `aws configure`).
    -   [Docker Desktop](https://www.docker.com/products/docker-desktop/).
    -   [Node.js](https://nodejs.org/) and [Java 17](https://adoptium.net/).
3.  **Source Code**:
    -   Clone the workshop repository:
        ```bash
        git clone https://github.com/your-repo/gametracker-workshop.git
        cd gametracker-workshop
        ```

---

**Note**: Some services like **RDS** and **NAT Gateway** charge hourly rates. Please follow the **Cleanup** section immediately after completing the workshop to avoid unexpected charges.
