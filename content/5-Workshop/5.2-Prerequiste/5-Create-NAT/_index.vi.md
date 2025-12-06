---
title: "Tạo NAT Gateway"
date: "2025-10-27"
weight: 5
chapter: false
pre: " <b> 5.2.5 </b> "
---

# Tạo NAT Gateway (Tùy chọn)

Nếu Lambda function trong private subnet cần truy cập internet (ví dụ: để cài đặt gói, gọi API bên ngoài, hoặc pull Docker image nếu không dùng endpoint), bạn cần có NAT Gateway.

**Lưu ý**: NAT Gateway tính phí theo giờ. Chỉ tạo khi cần thiết hoặc ngay trước khi deployment.

## 1. Cấp phát Elastic IP (EIP)

### CLI
```bash
aws ec2 allocate-address --domain vpc --region ap-southeast-2
# Lưu lại AllocationId
```

### AWS Console
1. Truy cập **VPC Dashboard** → **Elastic IPs**.
2. Nhấn **Allocate Elastic IP address**.
3. Region: `ap-southeast-2`.
4. Nhấn **Allocate**.

---

## 2. Tạo NAT Gateway

Chúng ta sẽ tạo NAT Gateway trong một trong các **Public Subnets**.

### CLI
```bash
aws ec2 create-nat-gateway \
  --subnet-id <SUBNET_PUBLIC_1_ID> \
  --allocation-id <EIP_ALLOCATION_ID> \
  --region ap-southeast-2
```

### AWS Console
1. Truy cập **NAT Gateways** → **Create NAT gateway**.
2. **Name**: `gametracker-nat`.
3. **Subnet**: Chọn `gametracker-public-1`.
4. **Elastic IP allocation ID**: Chọn EIP vừa tạo ở trên.
5. Nhấn **Create NAT gateway**.

---

## 3. Cập nhật Private Route Table

Định tuyến lưu lượng internet từ private subnet đi qua NAT Gateway.

### CLI
```bash
aws ec2 create-route \
  --route-table-id <RTB_PRIVATE_ID> \
  --destination-cidr-block 0.0.0.0/0 \
  --nat-gateway-id <NAT_GATEWAY_ID>
```

### AWS Console
1. Truy cập **Route Tables**.
2. Chọn `private-route-table-1`.
3. Vào tab **Routes** → **Edit routes**.
4. Thêm route:
   - **Destination**: `0.0.0.0/0`.
   - **Target**: Chọn `NAT Gateway` → `gametracker-nat`.
5. Nhấn **Save changes**.
