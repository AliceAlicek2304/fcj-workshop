---
title: "Introduction"
date: "2025-10-27"
weight: 1
chapter: false
pre: " <b> 5.1 </b> "
---

# Deploy GameTracker on AWS

## 🎯 Workshop Objective
In this workshop, we will manually deploy the **GameTracker** platform—a full-stack web application—to AWS from scratch. You will build a serverless-ready architecture using industry-standard services.

The goal is to create a production-like environment in the **Sydney (ap-southeast-2)** region, covering everything from networking to application deployment.

## 🏗️ Architecture Overview

The solution adopts a modern cloud-native architecture:
- **Frontend**: React Single Page Application (SPA) hosted on **Amazon S3** and distributed via **Amazon CloudFront**.
- **Backend**: Spring Boot application containerized with Docker, stored in **Amazon ECR**, and running serverless on **AWS Lambda** exposed via **API Gateway**.
- **Database**: **SQL Server Express** running on **Amazon RDS** for structured game data.
- **Network**: A custom **VPC** with public/private subnets and security groups to ensure isolation and security.

![Architecture](/images/2-Proposal/GameTracker1.jpg)

## 📋 Services Used
We will configure the following AWS services:

| Category | Services |
|----------|----------|
| **Networking** | VPC, Subnets, Internet Gateway, NAT Gateway (optional), Route53 |
| **Compute** | AWS Lambda, API Gateway (HTTP API) |
| **Storage** | Amazon S3 (Frontend & Assets) |
| **Database** | Amazon RDS (SQL Server) |
| **Container** | Amazon ECR (Elastic Container Registry) |
| **CDN & Security** | Amazon CloudFront, AWS WAF, IAM, Security Groups |

## 🚀 Deployment Steps
This workshop is divided into logical phases:

1.  **Network Setup**: Creating VPC, Subnets, and Routing.
2.  **Database Provisioning**: Setting up RDS SQL Server.
3.  **Backend Deployment**:
    - Creating an ECR Repository.
    - Building and pushing the Docker image.
    - Creating the Lambda function and connecting it to the database.
    - Exposing the backend via API Gateway.
4.  **Frontend Deployment**:
    - Creating S3 buckets.
    - Setting up CloudFront distribution.
    - Deploying the React application.
5.  **Clean up**: Instructions on how to decommission resources to avoid costs.

## �️ Prerequisites
- An active AWS Account.
- AWS CLI installed and configured.
- Docker installed locally.
- Basic knowledge of terminal commands.

---

**Note**: Some resources like **RDS** and **NAT Gateway** incur hourly costs. Please follow the **Cleanup** section immediately after finishing the workshop to avoid unexpected charges.
