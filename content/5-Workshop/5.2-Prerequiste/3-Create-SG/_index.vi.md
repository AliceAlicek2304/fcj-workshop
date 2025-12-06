---
title: "Tạo Security Groups"
date: "2025-10-27"
weight: 3
chapter: false
pre: " <b> 5.2.3 </b> "
---

# Tạo Security Groups

Security Groups cho phép chúng ta kiểm soát lưu lượng truy cập. Chúng ta cần hai nhóm: một cho lớp tính toán (Lambda) và một cho lớp cơ sở dữ liệu (RDS).

## 1. Tạo Lambda Security Group

### CLI
```bash
# Tạo Security Group
aws ec2 create-security-group \
  --group-name gametracker-lambda-sg \
  --description "SG for Lambda functions" \
  --vpc-id <VPC_ID>
  
# Lưu ý: Mặc định, SG cho phép tất cả lưu lượng đi ra (outbound), phù hợp với Lambda.
```

### AWS Console
1. Truy cập **EC2 Dashboard** → **Security Groups** → **Create security group**.
2. **Name**: `gametracker-lambda-sg`.
3. **Description**: SG for Lambda functions.
4. **VPC**: `gametracker-vpc`.
5. **Inbound rules**: Không có (Lambda không nhận kết nối trực tiếp trong kiến trúc này).
6. **Outbound rules**: Allow all traffic (Mặc định).
7. Nhấn **Create security group**.

---

## 2. Tạo RDS Security Group

Group này cho phép Lambda function kết nối tới cơ sở dữ liệu SQL Server trên cổng 1433.

### CLI
```bash
# Tạo Security Group
aws ec2 create-security-group \
  --group-name gametracker-rds-sg \
  --description "SG for RDS" \
  --vpc-id <VPC_ID>

# Thêm Inbound Rule cho SQL Server (Port 1433) từ Lambda SG
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
   - **Source**: Custom → Chọn `gametracker-lambda-sg` (gõ tên để tìm).
6. **Outbound rules**: Allow all traffic (Mặc định).
7. Nhấn **Create security group**.
