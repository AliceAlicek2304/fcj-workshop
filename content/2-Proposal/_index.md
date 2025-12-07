---
title: "Proposal"
date: "2025-09-10"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# 1. BACKGROUND AND MOTIVATION

## 1.1 EXECUTIVE SUMMARY
**Context**
The gaming industry is rapidly growing, with players seeking deeper engagement through data tracking and simulation tools. **GameTracker** is a cloud-native web application designed to empower players and administrators to manage, track, and share simplified information about game entities (characters, weapons, banners, events). The solution addresses the fragmentation of game data across wikis and spreadsheets by providing a centralized, localized platform.

**Core Features (MVP)**
1.  **Game Information Hub**: Centralized database for Character, Weapon, and Item attributes.
2.  **Gacha Simulator**: Realistic simulation of entry/wish systems to test drop rates.
3.  **Gacha History Tracker**: Tools to import pull history and analyze luck/pity.
4.  **Event Timeline**: Interactive roadmap of past, current, and upcoming events.

**In Development**
1.  **Real-time Resource Tracking**: Integration for real-time in-game currency/energy checks.
2.  **Notification System**: Alerts for resource overflow or event endings.

## 1.2 PROJECT SUCCESS CRITERIA
-   **Performance**: API latency < 200ms for 95% of requests.
-   **Availability**: 99.9% uptime during the first month of operation.
-   **Cost Efficiency**: Monthly AWS infrastructure cost remains under $150.

## 1.3 ASSUMPTIONS
-   **Access**: Development team has full administrative access to the AWS account.
-   **Third-Party Services**: Google OAuth2 services and Game APIs remain available and stable.
-   **Data Availability**: Game asset data (images, stats) can be manually sourced or imported without strict copyright blockers for educational/workshop purposes.
-   **Budget**: The project operates within the AWS Free Tier limitations where possible, with a budget cap for RDS and NAT Gateway.

# 2. SOLUTION ARCHITECTURE / ARCHITECTURAL DIAGRAM

## 2.1 TECHNICAL ARCHITECTURE DIAGRAM
The solution utilizes a serverless-first approach on AWS to ensure scalability and low maintenance.

![Architecture](/images/2-Proposal/GameTracker1.jpg)

**Components**:
-   **Frontend**: React (Vite) hosted on S3 + CloudFront.
-   **Backend**: Spring Boot on AWS Lambda + API Gateway.
-   **Database**: SQL Server on Amazon RDS.
-   **Security**: AWS WAF, IAM, Security Groups.

## 2.2 TECHNICAL PLAN
We will implement the solution using industry-standard DevOps practices:
-   **Frontend**: Developed with React and TypeScript. deployed to S3/CloudFront.
-   **Backend**: Spring Boot 3 Java application, containerized with Docker, pushed to ECR, and deployed to Lambda.
-   **Infrastructure**: Managed via AWS Console and CLI scripts for reproducibility.
-   **Testing**: Unit testing for backend logic and manual UAT for frontend flows.

## 2.3 PROJECT PLAN
The project follows a 4-week Agile timeline:
-   **Week 1**: Analysis, DB Schema Design, VPC Setup.
-   **Week 2**: Backend API Development & Database Connectivity.
-   **Week 3**: Frontend UI Implementation & Gacha Logic.
-   **Week 4**: Integration, CI/CD Pipeline, Deployment, and Documentation.

## 2.4 SECURITY CONSIDERATIONS
-   **Authentication**: Stateless authentication using JWT and Google OAuth2.
-   **Network Security**: VPC with Public/Private subnets; Database in private subnet; WAF protecting CloudFront.
-   **Encryption**: TLS 1.2+ for data in transit; RDS instances encrypted at rest.
-   **Access Control**: Least Privilege IAM roles for Lambda functions.

# 3. ACTIVITIES AND DELIVERABLES

## 3.1 ACTIVITIES AND DELIVERABLES
| Phase | Activities | Deliverables |
|-------|------------|--------------|
| **Setup** | VPC creation, IAM setup, Git repo init | AWS Environment, Architecture Doc |
| **Development** | Coding API endpoints, UI, DB migration | Source Code, Docker Images |
| **Deployment** | S3 sync, Lambda deployment, CloudFront config | Live URL, API Endpoint |

## 3.2 OUT OF SCOPE
-   **Mobile App**: Native iOS/Android versions are not included.
-   **Multiplayer**: Real-time multiplayer game servers or lobbies.
-   **Payment Processing**: No integration with payment gateways for real money.

## 3.3 PATH TO PRODUCTION
-   **Scalability**: Architecture supports 0-10,000 users via Lambda auto-scaling.
-   **Monitoring**: Amazon CloudWatch Dashboards for error rates and latency.
-   **Backup**: Automated RDS backups and S3 versioning enabled for disaster recovery.

# 4. EXPECTED AWS COST BREAKDOWN BY SERVICES
**Estimated Monthly Cost**: ~$123.00

| Service | Estimated Usage | Cost (Approx) |
|---------|-----------------|---------------|
| **RDS (SQL Server)** | db.t3.micro (Single AZ) | ~$60.00 |
| **NAT Gateway** | 1 Unit (if required) | ~$32.00 |
| **AWS WAF** | Web ACL + Request fees | ~$10.00 |
| **CloudFront** | 100GB Data Out | ~$8.50 |
| **AWS Lambda** | 1M Invocations | ~$5.00 |
| **Other** | S3, logs, Route53 | ~$7.50 |

# 5. TEAM

| Name | Role | Email | Responsibility |
|------|------|-------|----------------|
| **Nguyen Van Cuong** | Full Stack Developer | `cuongnvse183645@fpt.edu.vn` | End-to-end Implementation |

# 6. RESOURCES & COST ESTIMATES
*Labor costs (Educational/Workshop context)*

| Resource | Responsibility | Effort Estimate |
|----------|----------------|-----------------|
| Full Stack Developer | Design, Code, Deploy | ~160 Hours (4 Weeks) |
| Technical Mentor | Review, Guidance | ~20 Hours |

**Total Estimated Effort**: 4 Man-weeks.

# 7. ACCEPTANCE

The product is accepted upon demonstration of:
1.  **User Login**: Successful Google OAuth2 login.
2.  **Data Management**: CRUD operations for characters/weapons working.
3.  **Simulation**: Gacha simulator functioning with correct logic.
4.  **Deployment**: Application is publicly accessible via HTTPS.
5.  **Documentation**: Complete User Guide and Deployment Guide provided.

<br>

<h3 style="font-size: 1.3em;">🔗 Project Website: <a href="https://d2eu9it59oopt8.cloudfront.net/" target="_blank">https://d2eu9it59oopt8.cloudfront.net/</a></h3>
<h3 style="font-size: 1.3em;">📥 Download Proposal: <a href="/files/Proposal-TeamOne.docx" download>Proposal-TeamOne.docx</a></h3>
