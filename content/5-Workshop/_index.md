---
title: "Workshop: Deploy GameTracker on AWS"
date: "2025-10-27"
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Workshop: Deploy GameTracker on AWS

## Overview

Welcome to the **GameTracker Deployment Workshop**. In this hands-on session, you will learn how to deploy a complete 3-tier web application on AWS using modern cloud practices.

You will move from a local development environment to a production-ready cloud architecture.

### What you will build

You will deploy **GameTracker**, a web application that tracks player statistics. The architecture includes:
-   **Frontend**: React Single Page Application (SPA) hosted on **Amazon S3** and distributed via **Amazon CloudFront**.
-   **Backend**: Spring Boot REST API containerized with Docker, running on **AWS Lambda** (Serverless).
-   **Database**: **Amazon RDS for SQL Server** to store structured game data.
-   **Network**: A custom **VPC** with public/private subnets and security groups.

![Architecture](/images/1/0001.png?featherlight=false&width=90pc)

## Workshop Structure

This workshop is divided into the following modules:

1.  **[Introduction](5.1-introduce/)**: Overview of the project, architecture, and AWS services used.
2.  **[Prerequisites](5.2-prerequiste/)**: Setting up the foundation (VPC, IAM, Security Groups, NAT Gateway).
3.  **[Create Database](5.3-create-rds/)**: Provisioning the Amazon RDS SQL Server instance.
4.  **[Deploy Application](5.4-deploy-app/)**:
    -   Containerizing and deploying the Backend (ECR, Lambda, API Gateway).
    -   Hosting and distributing the Frontend (S3, CloudFront).
5.  **[Backup & Restore](6-backup/)**: Strategies for protecting your data.
6.  **[Cleanup](7-cleanup/)**: Removing resources to avoid costs.

## Prerequisites

Before starting, ensure you have:
-   An active **AWS Account**.
-   **AWS CLI** installed and configured.
-   **Docker** installed locally.
-   **Java 17+** and **Node.js** installed (for building the app).

Let's get started!
