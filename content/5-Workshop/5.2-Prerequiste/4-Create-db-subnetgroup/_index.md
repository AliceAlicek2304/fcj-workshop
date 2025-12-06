---
title: "Create DB Subnet Group"
date: "2025-10-27"
weight: 4
chapter: false
pre: " <b> 5.2.4 </b> "
---

# Create DB Subnet Group

The **DB Subnet Group** tells RDS which subnets it can use to deploy the database instances. For high availability, we must select subnets in at least two different Availability Zones.

## 1. Create DB Subnet Group

We will use our two **Private Subnets** for this group to ensure the database is not directly accessible from the internet.

### CLI
```bash
aws rds create-db-subnet-group \
  --db-subnet-group-name gametracker-db-subnet-group \
  --db-subnet-group-description "Private subnets for gametracker RDS" \
  --subnet-ids <SUBNET_PRIVATE_1_ID> <SUBNET_PRIVATE_2_ID>
```

### AWS Console
1. Open the [RDS Console](https://console.aws.amazon.com/rds).
2. In the navigation pane, click **Subnet groups**.
3. Click **Create DB subnet group**.
4. **Name**: `gametracker-db-subnet-group`.
5. **Description**: Private subnets for GameTracker.
6. **VPC**: Select `gametracker-vpc`.
7. **Add subnets**:
   - **Availability Zones**: Select `ap-southeast-2a` and `ap-southeast-2b`.
   - **Subnets**: Select the CIDRs corresponding to your **Private Subnets** (e.g., `10.10.2.0/24` and `10.10.3.0/24`).
8. Click **Create**.
