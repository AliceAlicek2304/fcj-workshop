---
title: "Tạo VPC & Network"
date: "2025-10-27"
weight: 1
chapter: false
pre: " <b> 5.2.1 </b> "
---

# Tạo VPC và Hạ tầng Mạng

Trong bước này, chúng ta sẽ thiết lập Virtual Private Cloud (VPC), nơi chứa các tài nguyên ứng dụng. Chúng ta sẽ tạo các public subnet cho các tài nguyên hướng internet và private subnet cho các tài nguyên nội bộ (như Lambda và RDS).

![VPC Architecture](/images/1/0001.png?featherlight=false&width=90pc)

## 1. Tạo VPC

### CLI
```bash
aws ec2 create-vpc \
  --cidr-block 10.10.0.0/16 \
  --tag-specifications 'ResourceType=vpc,Tags=[{Key=Name,Value=gametracker-vpc}]' \
  --region ap-southeast-2
```

### AWS Console
1. Mở [VPC Dashboard](https://console.aws.amazon.com/vpc).
2. Nhấn **Create VPC**.
3. **VPC settings**:
   - **Name tag**: `gametracker-vpc`
   - **IPv4 CIDR block**: `10.10.0.0/16`
4. Nhấn **Create VPC**.

---

## 2. Tạo Subnets

Chúng ta sẽ tạo 2 Public Subnets và 2 Private Subnets trên hai Availability Zones (AZs) để đảm bảo tính sẵn sàng cao.

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

# Bật Auto-assign Public IP cho Public Subnets
aws ec2 modify-subnet-attribute --subnet-id <SUBNET_PUBLIC_1_ID> --map-public-ip-on-launch
aws ec2 modify-subnet-attribute --subnet-id <SUBNET_PUBLIC_2_ID> --map-public-ip-on-launch
```

### AWS Console
1. Truy cập **Subnets** → **Create subnet**.
2. Chọn `gametracker-vpc`.
3. Tạo 4 subnets với CIDR và AZ như trên.
4. Với các **Public Subnets**: Chọn subnet → **Actions** → **Edit subnet settings** → Enable **Auto-assign public IPv4 address**.

---

## 3. Internet Gateway

### CLI
```bash
# Tạo IGW
aws ec2 create-internet-gateway --tag-specifications 'ResourceType=internet-gateway,Tags=[{Key=Name,Value=gametracker-igw}]'

# Gắn vào VPC
aws ec2 attach-internet-gateway --internet-gateway-id <IGW_ID> --vpc-id <VPC_ID>
```

### AWS Console
1. Truy cập **Internet Gateways** → **Create internet gateway**.
2. Name: `gametracker-igw`.
3. Nhấn **Create**.
4. Chọn IGW vừa tạo → **Actions** → **Attach to VPC** → Chọn `gametracker-vpc`.

---

## 4. Route Tables

### CLI
```bash
# Tạo Public Route Table
aws ec2 create-route-table --vpc-id <VPC_ID> --tag-specifications 'ResourceType=route-table,Tags=[{Key=Name,Value=public-route-table}]'

# Thêm Route ra Internet
aws ec2 create-route --route-table-id <RTB_PUBLIC_ID> --destination-cidr-block 0.0.0.0/0 --gateway-id <IGW_ID>

# Liên kết Public Subnets
aws ec2 associate-route-table --route-table-id <RTB_PUBLIC_ID> --subnet-id <SUBNET_PUBLIC_1_ID>
aws ec2 associate-route-table --route-table-id <RTB_PUBLIC_ID> --subnet-id <SUBNET_PUBLIC_2_ID>

# Tạo Private Route Table
aws ec2 create-route-table --vpc-id <VPC_ID> --tag-specifications 'ResourceType=route-table,Tags=[{Key=Name,Value=private-route-table-1}]'

# Liên kết Private Subnets
aws ec2 associate-route-table --route-table-id <RTB_PRIVATE_ID> --subnet-id <SUBNET_PRIVATE_1_ID>
aws ec2 associate-route-table --route-table-id <RTB_PRIVATE_ID> --subnet-id <SUBNET_PRIVATE_2_ID>
```

### AWS Console
1. Truy cập **Route Tables** → **Create route table**.
2. Tạo `public-route-table` và `private-route-table-1`.
3. **Public Route Table**:
   - **Routes** → Edit routes → Thêm `0.0.0.0/0` trỏ tới `gametracker-igw`.
   - **Subnet associations** → Edit → Chọn cả 2 public subnet.
4. **Private Route Table**:
   - **Subnet associations** → Edit → Chọn cả 2 private subnet.

---

## 5. VPC Endpoint cho S3

Cần thiết để Lambda trong private subnet truy cập S3 mà không cần NAT Gateway.

### CLI
```bash
aws ec2 create-vpc-endpoint \
  --vpc-id <VPC_ID> \
  --service-name com.amazonaws.ap-southeast-2.s3 \
  --route-table-ids <RTB_PUBLIC_ID> <RTB_PRIVATE_ID>
```

### AWS Console
1. Truy cập **Endpoints** → **Create endpoint**.
2. Name: `gametracker-s3-endpoint`.
3. Service category: **AWS services**.
4. Service: `com.amazonaws.ap-southeast-2.s3` (Gateway type).
5. VPC: `gametracker-vpc`.
6. Route tables: Chọn cả public và private route table.
7. Nhấn **Create endpoint**.
