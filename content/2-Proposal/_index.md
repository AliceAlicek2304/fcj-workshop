---
title: "Proposal"
date: "2025-09-10"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# 1. BACKGROUND AND MOTIVATION

## 1.1 EXECUTIVE SUMMARY
**Customer Background**
GameTracker is a platform designed for game players and admins to **manage, track, and share information** about characters, weapons, banners, items, and events.

**Business and Technical Objectives**
- **Unified Management**: Create a centralized system for managing game data effectively.
- **Accessibility**: Provide easy access to information for English-language games which can be a barrier for some users.
- **Efficiency**: Reduce manual maintenance time and improve data reliability for admins.
- **Scalability**: Build a system scalable to multiple games and community features using serverless architecture.

**Use Cases**
- **Players**: Track gacha history, simulate pulls, view banner/event timelines.
- **Admins**: Manage game data (CRUD) with clear access permissions.

**Partner Professional Services**
We will deliver a full-stack web application hosted on AWS, utilizing serverless technologies (Lambda, S3, RDS) to ensure low operational costs and high availability.

## 1.2 PROJECT SUCCESS CRITERIA
- **System Stability**: Stable, auto-scaling system with low maintenance costs.
- **Security**: Secure API with centralized data management and role-based access control.
- **User Engagement**: Functional gacha tools and timelines that help players track game events conveniently.
- **Scalability**: Architecture ready for easy expansion to support more games and features.

## 1.3 ASSUMPTIONS
- **Prerequisites**: AWS account access with necessary permissions for deployment.
- **Dependencies**: Third-party authentication (Google OAuth2).
- **Constraints**: Budget constraints requiring a low-cost serverless approach.
- **Risks**: Potential cold start latency with Lambda (mitigated by warmers), RDS costs (mitigated by instance selection).

# 2. SOLUTION ARCHITECTURE / ARCHITECTURAL DIAGRAM

## 2.1 TECHNICAL ARCHITECTURE DIAGRAM
**Proposed High-Level Architecture**:
The solution adopts a modern cloud-native architecture:
- **Frontend**: React SPA served via S3 + CloudFront, protected by AWS WAF.
- **Backend**: Spring Boot serverless deployed on AWS Lambda, using JWT and Google OAuth2 for auth.
- **Database**: SQL Server on AWS RDS.
- **Storage**: AWS S3 for storing static assets (avatars, backgrounds, weapons).
- **Security**: AWS WAF, IAM, and Spring Security.

![IoT Weather Station Architecture](/images/2-Proposal/GameTracker1.jpg)

**AWS Services Used**:
- AWS S3, AWS Lambda, AWS RDS, AWS CloudFront, AWS WAF, AWS SES, AWS IAM.

## 2.2 TECHNICAL PLAN
We will develop scripts using **AWS CDK/CloudFormation** or manual setup procedures documented for repeatability.
- **Frontend**: React, TypeScript, Vite.
- **Backend**: Spring Boot, Spring Security.
- **DevOps**: Docker, CI/CD pipelines.

All critical paths including user login, data synchronization, and gacha simulation will include extensive test coverage.

## 2.3 PROJECT PLAN
The project will follow an Agile methodology over a 1-month timeline.
- **Week 1**: Planning, Requirements Analysis, Architecture Design.
- **Week 2**: Backend Development (API, Auth, Database).
- **Week 3**: Frontend Development (UI/UX, Admin Dashboard, Tools).
- **Week 4**: Deployment, Testing, Documentation, and Handover.

## 2.4 SECURITY CONSIDERATIONS
**Best Practices Implemented**:
- **Identity**: Google OAuth2 integration and JWT for secure stateless authentication.
- **Infrastructure**: AWS WAF to protect against common web exploits.
- **Access Control**: Role-based access control (RBAC) for Admins vs Users.
- **Data Protection**: HTTPS encryption in transit; RDS encryption at rest.
- **Monitoring**: AWS CloudWatch for logs and metrics.

# 3. ACTIVITIES AND DELIVERABLES

## 3.1 ACTIVITIES AND DELIVERABLES

| Project Phase | Timeline | Activities | Deliverables/Milestones |
|---------------|----------|------------|-------------------------|
| **Assessment & Setup** | Week 1 | Requirement analysis, architecture design, AWS setup (S3, RDS, Lambda) | Architecture Diagram, AWS Environment Ready |
| **Backend Implementation** | Week 2 | Build Lambda functions, API endpoints, Auth integration, DB schema | Working API, Database connectivity |
| **Frontend Implementation** | Week 3 | React SPA development, Dashboard creation, Gacha tools logic | Functional Web UI, Admin Dashboard |
| **Testing & Go-live** | Week 4 | Integration testing, Security optimization, Deployment to CloudFront | Deployed Application, User Guide, Documentation |

## 3.2 OUT OF SCOPE
- Mobile Application development (iOS/Android native apps).
- Real-time multiplayer game server features (only web-based data management).
- Integration with game servers directly (data is manually managed/imported).

## 3.3 PATH TO PRODUCTION
The current proposal outlines the path to a production-ready MVP.
- **POC to Prod**: The system is designed to be production-grade from the start using AWS managed services.
- **Gaps**: Further load testing and fine-tuning of WAF rules may be needed based on actual traffic patterns.
- **Operations**: Error handling and monitoring are implemented via CloudWatch.

# 4. EXPECTED AWS COST BREAKDOWN BY SERVICES

**Estimated Monthly Cost**: ~$121-123/month

- **AWS Lambda**: ~$5-7 (Memory: 3008 MB, ~12k invocations).
- **S3 Standard**: ~$0.23 (10 GB storage).
- **CloudFront**: ~$8.50 (100 GB egress).
- **RDS (SQL Server)**: ~$60+ (db.t3.medium or similar).
- **AWS WAF**: ~$10 (Web ACL + requests).
- **NAT Gateway**: ~$32 (if required for Lambda in VPC).
- **Others (SES, Route53, CloudWatch)**: ~$6.

*Note: Costs are estimates and depend on actual usage and region.*

# 5. TEAM

**Partner Project Team**
| Name | Title | Role | Email / Contact Info |
|------|-------|------|----------------------|
| [Name] | Delivery Manager | Project Manager | [Email] |
| [Name] | Sr. Solutions Architect | Technical Lead | [Email] |

**Project Stakeholders**
| Name | Title | Stakeholder for | Email / Contact Info |
|------|-------|-----------------|----------------------|
| [Name] | [Title] | [Role] | [Email] |

# 6. RESOURCES & COST ESTIMATES

| Resource | Responsibility | Rate (USD) / Hour |
|----------|----------------|-------------------|
| Solution Architect | System Design & Lead | - |
| Full-stack Engineer | Implementation | - |

**Total Estimated Effort**: [Total Man-days]

# 7. ACCEPTANCE

Upon completion of a Phase, the Partner will submit the associated tangible Deliverables to the Customer. The Customer will review, evaluate, and test the Deliverables within **eight (8) business days** (the “Acceptance Period”) to determine satisfaction of acceptance criteria.

If the Deliverable satisfies its acceptance criteria, Customer will furnish a written acceptance. If rejected, Customer will indicate detailed reasons, and Partner will correct defects. If no rejection is received within the Acceptance Period, Deliverables are deemed accepted.

<br>

<h3 style="font-size: 1.3em;">🔗 Project Website: <a href="https://d2eu9it59oopt8.cloudfront.net/" target="_blank">https://d2eu9it59oopt8.cloudfront.net/</a></h3>
