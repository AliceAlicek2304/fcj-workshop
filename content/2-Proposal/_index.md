---
title: "Proposal"
date: "2025-09-10"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# 1. PROJECT BACKGROUND

## 1.1 EXECUTIVE SUMMARY
**Context**
The gaming industry is rapidly growing, with players seeking deeper engagement through data tracking and simulation tools. **GameTracker** is a comprehensive platform designed to empower players and administrators to manage, track, and share simplified information about game entities (characters, weapons, banners, events).

**Problem Statement**
-   **Fragmentation**: Game data is often scattered across wikis and spreadsheets.
-   **Accessibility**: Many global games lack localized or easy-to-access data for non-native English speakers.
-   **Inefficiency**: Manual data entry for game admins is error-prone and time-consuming.

**Proposed Solution**
Use **GameTracker**, a cloud-native web application hosted on AWS. It leverages serverless technologies to provide a cost-effective, high-availability solution for tracking game statistics and simulating gacha mechanics.

## 1.2 FUNCTIONAL SCOPE

The system is designed with a core set of features ready for deployment, alongside a roadmap for advanced capabilities.

### ✅ Current Features (MVP)
1.  **Game Information Hub**: A centralized database allowing users to view detailed attributes of Characters, Weapons, and Items.
2.  **Gacha Simulator**: A realistic simulation of the game's "wish" system, allowing users to test drop rates without spending real currency.
3.  **Gacha History Tracker**: customized tools to import and visualize a player's actual pull history, generating statistics on luck and pity count.
4.  **Event Timeline**: An interactive visual roadmap displaying past, current, and upcoming game events to help players plan their resources.

### 🚧 In Development (Future Roadmap)
1.  **Real-time Resource Tracking**: Direct integration to verify in-game resources (e.g., Energy/Resin, Currency) in real-time.
2.  **Notification System**: Alerts for resin overflow or banner endings.

---

# 2. SOLUTION ARCHITECTURE

## 2.1 HIGH-LEVEL ARCHITECTURE
The solution is built on the **AWS Architecture Well-Architected Framework**, focusing on Reliability and Cost Optimization.

**Architecture Diagram**:

![Architecture](/images/2-Proposal/GameTracker1.jpg)

**Core Components**:
1.  **Frontend (Presentation Layer)**:
    -   Built with **React (Vite)** for a responsive SPA experience.
    -   Hosted on **Amazon S3** and delivered globally via **Amazon CloudFront** for low latency.
    -   Protected by **AWS WAF** against common web exploits.

2.  **Backend (Logic Layer)**:
    -   **Spring Boot** application containerized with **Docker**.
    -   Deployed on **AWS Lambda** (Serverless) to eliminate server management.
    -   Exposed via **API Gateway (HTTP API)** for secure and scalable RESTful endpoints.

3.  **Data Persistence (Data Layer)**:
    -   **Amazon RDS (SQL Server Express)**: Stores structured relational data (User profiles, Character stats, Gacha history).
    -   **Amazon S3**: Stores static assets (Character avatars, Weapon icons) with high durability.

4.  **Security & Identity**:
    -   **Google OAuth2**: Secure, password-less authentication for users.
    -   **AWS IAM**: Granular permission management for all AWS resources.
    -   **Security Groups**: Virtual firewalls controlling traffic at the instance level.

## 2.2 TECHNOLOGY STACK
-   **Languages**: Java 17, TypeScript/JavaScript.
-   **Frameworks**: Spring Boot 3, React 18.
-   **DevOps**: Docker, AWS CLI.
-   **Database**: Microsoft SQL Server 2022.

---

# 3. IMPLEMENTATION PLAN

## 3.1 MILESTONES
The project is executed in a 4-week Agile sprint:

| Phase | Timeline | Activities | Deliverables |
|-------|----------|------------|--------------|
| **1. Analysis & Design** | Week 1 | Requirement gathering, DB Schema design, AWS VPC setup | Architecture Blueprint, AWS Environment |
| **2. Backend Development** | Week 2 | API Development, Auth integration, DB Connectivity | Functional REST API, Swagger Docs |
| **3. Frontend Development** | Week 3 | UI Integration, Gacha Logic, Dashboard implementation | Complete Web Application |
| **4. DevOps & Handoff** | Week 4 | CI/CD pipeline (GitHub Actions), Testing, Documentation | User Guide, Admin Manual, Live Site |

## 3.2 PATH TO PRODUCTION
-   **Environment**: Analyzing Development vs. Production environments.
-   **Scalability**: The serverless design allows handling 0 to 10,000 concurrent users without manual intervention.
-   **Monitoring**: Integrated **Amazon CloudWatch** for real-time log monitoring and error alerting.

---

# 4. COST ESTIMATION
**Estimated Monthly Cost (AWS)**: ~$123.00

| Service | Estimated Usage | Cost (Approx) |
|---------|-----------------|---------------|
| **RDS (SQL Server)** | db.t3.micro (Single AZ) | ~$60.00 |
| **NAT Gateway** | 1 Unit (if required) | ~$32.00 |
| **AWS WAF** | Web ACL + Request fees | ~$10.00 |
| **CloudFront** | 100GB Data Transfer Out | ~$8.50 |
| **AWS Lambda** | 1M Invocations | ~$5.00 |
| **Other (S3, logs)** | Standard tiers | ~$7.50 |

*Note: Costs can be optimized further by managing NAT Gateway and RDS usage hours.*

---

# 5. PROJECT TEAM

The project is delivered by a dedicated Full Stack Engineer responsible for the end-to-end lifecycle.

| Name | Role | Contact Email | Responsibility |
|------|------|---------------|----------------|
| **Nguyen Van Cuong** | Full Stack Developer | `cuongnvse183645@fpt.edu.vn` | System Architecture, Frontend/Backend Implementation, DevOps, Deployment |

---

# 6. ACCEPTANCE CRITERIA

The product will be accepted based on the successful demonstration of the following core flows:
1.  **User Login**: Successful authentication via Google.
2.  **Data Management**: Admin can Create/Read/Update/Delete game characters via the Dashboard.
3.  **Simulation**: Gacha simulator produces random results based on defined probability logic.
4.  **Deployment**: The application is accessible via the public CloudFront domain.

<br>

<h3 style="font-size: 1.3em;">🔗 Project Website: <a href="https://d2eu9it59oopt8.cloudfront.net/" target="_blank">https://d2eu9it59oopt8.cloudfront.net/</a></h3>
