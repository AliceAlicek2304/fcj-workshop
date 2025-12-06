---
title: "Tạo DB Subnet Group"
date: "2025-10-27"
weight: 4
chapter: false
pre: " <b> 5.2.4 </b> "
---

# Tạo DB Subnet Group

**DB Subnet Group** cho RDS biết những subnet nào có thể được sử dụng để triển khai các instance cơ sở dữ liệu. Để đảm bảo tính sẵn sàng cao (High Availability), chúng ta phải chọn các subnet nằm trong ít nhất hai Availability Zones khác nhau.

## 1. Tạo DB Subnet Group

Chúng ta sẽ sử dụng hai **Private Subnets** cho group này để đảm bảo database không thể truy cập trực tiếp từ internet.

### CLI
```bash
aws rds create-db-subnet-group \
  --db-subnet-group-name gametracker-db-subnet-group \
  --db-subnet-group-description "Private subnets for gametracker RDS" \
  --subnet-ids <SUBNET_PRIVATE_1_ID> <SUBNET_PRIVATE_2_ID>
```

### AWS Console
1. Mở [RDS Console](https://console.aws.amazon.com/rds).
2. Ở thanh điều hướng bên trái, chọn **Subnet groups**.
3. Nhấn **Create DB subnet group**.
4. **Name**: `gametracker-db-subnet-group`.
5. **Description**: Private subnets for GameTracker.
6. **VPC**: Chọn `gametracker-vpc`.
7. **Add subnets**:
   - **Availability Zones**: Chọn `ap-southeast-2a` và `ap-southeast-2b`.
   - **Subnets**: Chọn các CIDR tương ứng với **Private Subnets** của bạn (ví dụ: `10.10.2.0/24` và `10.10.3.0/24`).
8. Nhấn **Create**.
