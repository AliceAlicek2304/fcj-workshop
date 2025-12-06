---
title: "Tạo Cơ sở dữ liệu RDS"
date: "2025-10-27"
weight: 3
chapter: false
pre: " <b> 5.3 </b> "
---

# Tạo RDS SQL Server

Trong bước này, chúng ta sẽ tạo instance cơ sở dữ liệu **Microsoft SQL Server** để lưu trữ dữ liệu game. Chúng ta sẽ sử dụng phiên bản **SQL Server Express** vì nó đủ dùng và nằm trong gói AWS Free Tier.

## 1. Tạo RDS Instance

### CLI
```bash
# Tạo RDS Instance
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
1. Mở [RDS Console](https://console.aws.amazon.com/rds).
2. Nhấn **Create database**.
3. **Choose a database creation method**: Standard create.
4. **Engine options**: Microsoft SQL Server.
5. **Edition**: SQL Server Express Edition.
6. **Templates**: Chọn **Free tier**.
7. **Settings**:
   - **DB instance identifier**: `gametracker-mssql`.
   - **Master username**: `admin` (hoặc tên đăng nhập tùy chọn).
   - **Master password**: Nhập mật khẩu mạnh.
8. **Instance configuration**: `db.t3.micro`.
9. **Storage**: 20 GiB (General Purpose SSD gp2/gp3).
10. **Connectivity**:
    - **VPC**: `gametracker-vpc`.
    - **Subnet group**: `gametracker-db-subnet-group`.
    - **Public access**: **No**.
    - **VPC security group**: Choose existing -> `gametracker-rds-sg`.
11. **Additional configuration**:
    - **Initial database name**: (SQL Server không hỗ trợ tạo qua console, ta sẽ tạo sau).
12. Nhấn **Create database**.

---

## 2. Xác nhận tạo thành công

Đợi trạng thái chuyển từ **Creating** sang **Available**.

- **Endpoint**: Copy địa chỉ endpoint (ví dụ: `gametracker-mssql.xxxx.ap-southeast-2.rds.amazonaws.com`).
- **Port**: 1433.

Chúng ta sẽ sử dụng các thông tin này khi triển khai ứng dụng backend.
