---
title: "Create Security Groups"
date: "2025-10-27"
weight: 3
chapter: false
pre: " <b> 5.2.3 </b> "
---

# Create Security Groups

Security Groups allow us to control traffic. We need two groups: one for our Compute layer (Lambda) and one for our Database layer (RDS).

## 1. Create Lambda Security Group

### CLI
```bash
# Create Security Group
aws ec2 create-security-group \
  --group-name gametracker-lambda-sg \
  --description "SG for Lambda functions" \
  --vpc-id <VPC_ID>
  
# Note: By default, SGs allow all outbound traffic, which is what we want for Lambda.
```

### AWS Console
1. Navigate to **EC2 Dashboard** → **Security Groups** → **Create security group**.
2. **Name**: `gametracker-lambda-sg`.
3. **Description**: SG for Lambda functions.
4. **VPC**: `gametracker-vpc`.
5. **Inbound rules**: None (Lambda doesn't listen to incoming ports directly in this setup).
6. **Outbound rules**: Allow all traffic (Default).
7. Click **Create security group**.

---

## 2. Create RDS Security Group

This group allows the Lambda function to talk to the SQL Server database on port 1433.

### CLI
```bash
# Create Security Group
aws ec2 create-security-group \
  --group-name gametracker-rds-sg \
  --description "SG for RDS" \
  --vpc-id <VPC_ID>

# Add Inbound Rule for SQL Server (Port 1433) from Lambda SG
aws ec2 authorize-security-group-ingress \
  --group-id <RDS_SG_ID> \
  --protocol tcp \
  --port 1433 \
  --source-group <LAMBDA_SG_ID>
```

### AWS Console
1. **Security Groups** → **Create security group**.
2. **Name**: `gametracker-rds-sg`.
3. **Description**: SG for RDS.
4. **VPC**: `gametracker-vpc`.
5. **Inbound rules**:
   - **Type**: MS SQL.
   - **Port**: 1433.
   - **Source**: Custom → Select `gametracker-lambda-sg` (start typing the name to find it).
6. **Outbound rules**: Allow all traffic (Default).
7. Click **Create security group**.
