---
title: "Create VPC & Network"
date: "2025-10-27"
weight: 1
chapter: false
pre: " <b> 5.2.1 </b> "
---

# Create VPC and Network Infrastructure

In this step, we will set up the Virtual Private Cloud (VPC) where our application resources will reside. We will create public subnets for internet-facing resources (like load balancers or NAT gateways) and private subnets for internal resources (like Lambda and RDS).

![VPC Architecture](/images/1/0001.png?featherlight=false&width=90pc)

## 1. Create VPC

### CLI
```bash
aws ec2 create-vpc \
  --cidr-block 10.10.0.0/16 \
  --tag-specifications 'ResourceType=vpc,Tags=[{Key=Name,Value=gametracker-vpc}]' \
  --region ap-southeast-2
```

### AWS Console
1. Open the [VPC Dashboard](https://console.aws.amazon.com/vpc).
2. Click **Create VPC**.
3. **VPC settings**:
   - **Name tag**: `gametracker-vpc`
   - **IPv4 CIDR block**: `10.10.0.0/16`
4. Click **Create VPC**.

---

## 2. Create Subnets

We will create 2 Public Subnets and 2 Private Subnets across two Availability Zones (AZs) for high availability.

### CLI
```bash
# Public Subnet 1 (AZ A)
aws ec2 create-subnet --vpc-id <VPC_ID> --cidr-block 10.10.0.0/24 --availability-zone ap-southeast-2a --tag-specifications 'ResourceType=subnet,Tags=[{Key=Name,Value=gametracker-public-1}]'

# Public Subnet 2 (AZ B)
aws ec2 create-subnet --vpc-id <VPC_ID> --cidr-block 10.10.1.0/24 --availability-zone ap-southeast-2b --tag-specifications 'ResourceType=subnet,Tags=[{Key=Name,Value=gametracker-public-2}]'

# Private Subnet 1 (AZ A)
aws ec2 create-subnet --vpc-id <VPC_ID> --cidr-block 10.10.2.0/24 --availability-zone ap-southeast-2a --tag-specifications 'ResourceType=subnet,Tags=[{Key=Name,Value=gametracker-private-1}]'

# Private Subnet 2 (AZ B)
aws ec2 create-subnet --vpc-id <VPC_ID> --cidr-block 10.10.3.0/24 --availability-zone ap-southeast-2b --tag-specifications 'ResourceType=subnet,Tags=[{Key=Name,Value=gametracker-private-2}]'

# Enable Auto-assign Public IP for Public Subnets
aws ec2 modify-subnet-attribute --subnet-id <SUBNET_PUBLIC_1_ID> --map-public-ip-on-launch
aws ec2 modify-subnet-attribute --subnet-id <SUBNET_PUBLIC_2_ID> --map-public-ip-on-launch
```

### AWS Console
1. Navigate to **Subnets** → **Create subnet**.
2. Select your `gametracker-vpc`.
3. Create the 4 subnets with the CIDRs and AZs listed above.
4. For the **Public Subnets**: Select the subnet → **Actions** → **Edit subnet settings** → Enable **Auto-assign public IPv4 address**.

---

## 3. Internet Gateway

### CLI
```bash
# Create IGW
aws ec2 create-internet-gateway --tag-specifications 'ResourceType=internet-gateway,Tags=[{Key=Name,Value=gametracker-igw}]'

# Attach to VPC
aws ec2 attach-internet-gateway --internet-gateway-id <IGW_ID> --vpc-id <VPC_ID>
```

### AWS Console
1. Navigate to **Internet Gateways** → **Create internet gateway**.
2. Name: `gametracker-igw`.
3. Click **Create**.
4. Select the created IGW → **Actions** → **Attach to VPC** → Select `gametracker-vpc`.

---

## 4. Route Tables

### CLI
```bash
# Create Public Route Table
aws ec2 create-route-table --vpc-id <VPC_ID> --tag-specifications 'ResourceType=route-table,Tags=[{Key=Name,Value=public-route-table}]'

# Add Route to Internet
aws ec2 create-route --route-table-id <RTB_PUBLIC_ID> --destination-cidr-block 0.0.0.0/0 --gateway-id <IGW_ID>

# Associate Public Subnets
aws ec2 associate-route-table --route-table-id <RTB_PUBLIC_ID> --subnet-id <SUBNET_PUBLIC_1_ID>
aws ec2 associate-route-table --route-table-id <RTB_PUBLIC_ID> --subnet-id <SUBNET_PUBLIC_2_ID>

# Create Private Route Table
aws ec2 create-route-table --vpc-id <VPC_ID> --tag-specifications 'ResourceType=route-table,Tags=[{Key=Name,Value=private-route-table-1}]'

# Associate Private Subnets
aws ec2 associate-route-table --route-table-id <RTB_PRIVATE_ID> --subnet-id <SUBNET_PRIVATE_1_ID>
aws ec2 associate-route-table --route-table-id <RTB_PRIVATE_ID> --subnet-id <SUBNET_PRIVATE_2_ID>
```

### AWS Console
1. Navigate to **Route Tables** → **Create route table**.
2. Create `public-route-table` and `private-route-table-1`.
3. **Public Route Table**:
   - **Routes** → Edit routes → Add `0.0.0.0/0` targeting `gametracker-igw`.
   - **Subnet associations** → Edit → Select both public subnets.
4. **Private Route Table**:
   - **Subnet associations** → Edit → Select both private subnets.

---

## 5. VPC Endpoint for S3

Required for Lambda in private subnets to access S3 without NAT Gateway.

### CLI
```bash
aws ec2 create-vpc-endpoint \
  --vpc-id <VPC_ID> \
  --service-name com.amazonaws.ap-southeast-2.s3 \
  --route-table-ids <RTB_PUBLIC_ID> <RTB_PRIVATE_ID>
```

### AWS Console
1. Navigate to **Endpoints** → **Create endpoint**.
2. Name: `gametracker-s3-endpoint`.
3. Service category: **AWS services**.
4. Service: `com.amazonaws.ap-southeast-2.s3` (Gateway type).
5. VPC: `gametracker-vpc`.
6. Route tables: Select both public and private route tables.
7. Click **Create endpoint**.
