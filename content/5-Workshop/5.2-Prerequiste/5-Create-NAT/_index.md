---
title: "Create NAT Gateway"
date: "2025-10-27"
weight: 5
chapter: false
pre: " <b> 5.2.5 </b> "
---

# Create NAT Gateway (Optional)

If your Lambda function in the private subnet needs to access the internet (e.g., for installing packages, calling external APIs, or pulling Docker images if endpoints aren't used), you need a NAT Gateway.

**Note**: NAT Gateway incurs hourly costs. Only create if necessary or just before deployment.

## 1. Allocate Elastic IP (EIP)

### CLI
```bash
aws ec2 allocate-address --domain vpc --region ap-southeast-2
# Save the AllocationId
```

### AWS Console
1. Navigate to **VPC Dashboard** → **Elastic IPs**.
2. Click **Allocate Elastic IP address**.
3. Region: `ap-southeast-2`.
4. Click **Allocate**.

---

## 2. Create NAT Gateway

We will create the NAT Gateway in one of our **Public Subnets**.

### CLI
```bash
aws ec2 create-nat-gateway \
  --subnet-id <SUBNET_PUBLIC_1_ID> \
  --allocation-id <EIP_ALLOCATION_ID> \
  --region ap-southeast-2
```

### AWS Console
1. Navigate to **NAT Gateways** → **Create NAT gateway**.
2. **Name**: `gametracker-nat`.
3. **Subnet**: Select `gametracker-public-1`.
4. **Elastic IP allocation ID**: Select the EIP created above.
5. Click **Create NAT gateway**.

---

## 3. Update Private Route Table

Limit internet traffic from private subnets to go through the NAT Gateway.

### CLI
```bash
aws ec2 create-route \
  --route-table-id <RTB_PRIVATE_ID> \
  --destination-cidr-block 0.0.0.0/0 \
  --nat-gateway-id <NAT_GATEWAY_ID>
```

### AWS Console
1. Navigate to **Route Tables**.
2. Select `private-route-table-1`.
3. Go to **Routes** tab → **Edit routes**.
4. Add route:
   - **Destination**: `0.0.0.0/0`.
   - **Target**: Select `NAT Gateway` → `gametracker-nat`.
5. Click **Save changes**.
