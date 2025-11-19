---
title: "Proposal"
date: "2025-09-10"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# GameTracker Platform for Game Community
## A Unified AWS Serverless Solution for Game Data Management & Sharing

### 1. Executive Summary
GameTracker is a platform designed for game players and admins to **manage, track, and share information** about characters, weapons, banners, items, and events. The system supports multi-method login (email/password, Google OAuth2), account management, admin dashboard, and file storage on **AWS S3**.  

Frontend is a **React SPA** served via **S3 + CloudFront**, protected by **AWS WAF** to ensure security and performance. Backend is **Spring Boot serverless** deployed on **AWS Lambda** connected to **SQL Server (RDS)**.  

GameTracker provides **visual tools**:  

- **Gacha history tracker** for accounts, easy to view and analyze  
- **Gacha simulator** to predict pulls  
- **Banner/event timeline** showing event info and duration  

These tools help players manage game data effectively, especially for **English-language games**, which are difficult for some users to understand.  

---

### 2. Problem Statement
**Current Problem**  
Players face difficulty managing and accessing game data, especially in complex gacha games. Language barriers in English games make information less accessible.  

**Solution**  
GameTracker offers a **centralized, user-friendly system** where users can:  

- Manage and update game data  
- Track gacha history and simulate pulls  
- View banner and event timelines  

Admins can efficiently control content with **CRUD operations and clear access permissions**.  

**Benefits and ROI**  
- Optimized data management for users and admins  
- Reduced manual maintenance time, improved data reliability  
- Low operational costs via AWS serverless & S3  
- Scalable to multiple games and community features  

---

### 3. Solution Architecture
**Cloud-based modern architecture**:  

- **Frontend:** React SPA, served via S3 + CloudFront, SPA fallback, protected by **AWS WAF**  
- **Backend:** Spring Boot serverless on **AWS Lambda**, JWT auth, Google OAuth2, API protected by WAF  
- **Database:** SQL Server (**AWS RDS**)  
- **File Storage:** AWS S3 (avatars, backgrounds, weapons, banners)  
- **Admin Dashboard:** Full CRUD, role-based access control  
- **Security:** Spring Security, CORS, AWS WAF 

![IoT Weather Station Architecture](/images/2-Proposal/GameTracker.jpg)

**AWS Services Used**  
- AWS S3: store static files and media  
- AWS Lambda: serverless backend  
- AWS RDS: game data storage  
- AWS CloudFront: SPA distribution  
- AWS WAF: protect frontend & API  
- AWS SES: email verification and password reset  
- AWS IAM: manage access rights  

**Component Design**  
- **User:** register, login, manage account, avatar  
- **Admin:** manage game data, CRUD, access control  
- **Game Data:** characters, weapons, banners, echo, setecho, roles, elements, backgrounds  
- **Tools:** gacha tracker, gacha simulator, banner/event timeline  

---

### 4. Technical Implementation
**Implementation Phases**  
1. Requirements analysis and architecture design  
2. Backend development with Spring Boot serverless, JWT, Google OAuth2, RDS integration  
3. Frontend development with React SPA, admin dashboard, gacha tools and timeline  
4. AWS deployment: S3, CloudFront, SPA fallback, WAF  
5. Testing, security optimization, documentation  

**Technical Requirements**  
- Frontend: React, TypeScript, Vite, SPA fallback  
- Backend: Spring Boot, Spring Security, JWT, Google OAuth2, Lambda serverless  
- Database: SQL Server (RDS)  
- Cloud: S3, CloudFront, Lambda, WAF, SES  
- DevOps: Docker, CI/CD, AWS IAM  

---

### 5. Timeline & Milestones (1 Month)
| Week | Phase | Tasks |
|------|-------|-------|
| Week 1 | Planning & Setup | Requirement analysis, architecture, AWS preparation (S3, RDS, Lambda, WAF, CloudFront) |
| Week 2 | Backend Development | Build backend, JWT, Google OAuth2, API endpoints, connect RDS, deploy Lambda & WAF |
| Week 3 | Frontend Development | Build React SPA, admin dashboard, gacha tools, timeline banner/event |
| Week 4 | Deployment & Testing | Deploy SPA to S3 + CloudFront, SPA fallback, WAF, testing, optimize security, complete documentation |

---

### 6. Budget Estimation (summary)

- AWS Lambda — Memory: 3008 MB ~ $5/month.
- S3 Standard — 10 GB storage ~ $0.23/month.
- CloudFront — 100 GB egress ~ $8.50/month.
- RDS (SQL Server, production) ~ $60+/month.
- SES — Approx: ~ $0.01/month.
- CloudWatch — Logs/metrics (10 GB logs) ~ $5/month.
- AWS WAF — Web ACL + 1M requests ~ $10/month.
- Route53 — 1 hosted zone + 1M queries ~ $0.90/month.
- Total = $89.64/month

---


### 7. Risk Assessment
- AWS downtime: Medium impact, low probability  
- Security attack: High impact, low probability  
- Increased costs: Medium impact, medium probability
- Data errors due to admin input: Medium impact, low probability  

**Mitigation strategies**  
- Use AWS WAF, IAM for access control, HTTPS, secure JWT  
- Monitor costs with CloudWatch, optimize queries and caching  
- Use RDS Multi-AZ, CloudFront CDN, fast rollback on errors  

**Contingency plan**  
- RDS failover in case of incidents 
- Rollback backend using Lambda Versioning

---


### 8. Expected Outcomes
- Stable, auto-scaling system with low cost
- Secure API, centralized and easy-to-manage data
- Easy to expand for more games and features
- Gacha tools and timeline help players track conveniently

---

<h3 style="font-size: 1.3em;">🔗 Project Website: <a href="https://d2eu9it59oopt8.cloudfront.net/" target="_blank">https://d2eu9it59oopt8.cloudfront.net/</a></h3>
