---
title: "Create RDS Database"
date: "2025-10-27"
weight: 3
chapter: false
pre: " <b> 5.3 </b> "
---

# Create RDS SQL Server

In this step, we will create the **Microsoft SQL Server** database instance that will store our game data. We will use the **SQL Server Express** edition which is eligible for the AWS Free Tier.

## 1. Create RDS Instance

### CLI
```bash
# Create RDS Instance
aws rds create-db-instance \
  --db-instance-identifier gametracker-mssql \
  --db-instance-class db.t3.micro \
  --engine sqlserver-ex \
  --master-username admin \
  --master-user-password YourSecurePassword123 \
  --allocated-storage 20 \
  --vpc-security-group-ids <RDS_SG_ID> \
  --db-subnet-group-name gametracker-db-subnet-group \
  --backup-retention-period 7 \
  --no-publicly-accessible \
  --region ap-southeast-2
```

### AWS Console
1. Open the [RDS Console](https://console.aws.amazon.com/rds).
2. Click **Create database**.
3. **Choose a database creation method**: Standard create.
4. **Engine options**: Microsoft SQL Server.
5. **Edition**: SQL Server Express Edition.
6. **Templates**: Select **Free tier**.
7. **Settings**:
   - **DB instance identifier**: `gametracker-mssql`.
   - **Master username**: `admin` (or your preferred username).
   - **Master password**: Enter a strong password.
8. **Instance configuration**: `db.t3.micro`.
9. **Storage**: 20 GiB (General Purpose SSD gp2/gp3).
10. **Connectivity**:
    - **VPC**: `gametracker-vpc`.
    - **Subnet group**: `gametracker-db-subnet-group`.
    - **Public access**: **No**.
    - **VPC security group**: Choose existing -> `gametracker-rds-sg`.
11. **Additional configuration**:
    - **Initial database name**: (SQL Server doesn't support this via console, we create it later via query).
12. Click **Create database**.

---

## 2. Verify creation

Wait for the status to change from **Creating** to **Available**.

- **Endpoint**: Copy the endpoint (e.g., `gametracker-mssql.xxxx.ap-southeast-2.rds.amazonaws.com`).
- **Port**: 1433.

We will use these details when deploying the backend application.
