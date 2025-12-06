---
title: "Dọn dẹp tài nguyên"
date: "2025-10-27"
weight: 7
chapter: false
pre: " <b> 5.7 </b> "
---

# Dọn dẹp tài nguyên

**Quan trọng**: Để tránh các chi phí không mong muốn, bạn bắt buộc phải xóa tất cả các tài nguyên đã tạo trong workshop này. Hãy làm theo các bước dưới đây theo đúng thứ tự.

## 1. Xóa Tài nguyên Ứng dụng

1.  **Frontend (S3 & CloudFront)**:
    -   **CloudFront**: Disable (Vô hiệu hóa) distribution -> Đợi nó deploy xong -> Xóa nó.
    -   **S3 Buckets**: Làm trống (Empty) các bucket `gametracker-frontend` và `gametracker-assets`, sau đó xóa chúng.

2.  **Backend (Lambda & API Gateway & ECR)**:
    -   **API Gateway**: Xóa API `gametracker-api`.
    -   **Lambda**: Xóa function `gametracker-api`.
    -   **ECR**: Xóa repository `gametracker-backend`.

## 2. Xóa Cơ sở dữ liệu

1.  **RDS Instance**:
    -   Truy cập **Amazon RDS** > **Databases**.
    -   Chọn `gametracker-mssql`.
    -   Action > **Delete**.
    -   Bỏ chọn **Create final snapshot** và xác nhận xóa.
2.  **DB Subnet Group**:
    -   Vào **Subnet groups** -> Xóa `gametracker-db-subnet-group`.

## 3. Xóa Tài nguyên Mạng

1.  **NAT Gateway** (Rất tốn phí!):
    -   Vào **VPC** > **NAT Gateways**.
    -   Xóa `gametracker-nat`.
    -   Đợi trạng thái chuyển sang `Deleted`.
2.  **Elastic IP**:
    -   Vào **Elastic IPs** -> Release (Giải phóng) IP đã cấp.
3.  **VPC Endpoint**:
    -   Vào **Endpoints** -> Xóa `gametracker-s3-endpoint`.
4.  **VPC**:
    -   Vào **Your VPCs** -> Chọn `gametracker-vpc` -> Actions -> **Delete VPC**.
    -   Việc này sẽ tự động xóa Subnets, Route Tables, Internet Gateway, và Security Groups liên quan.

## 4. Xác minh

Kiểm tra **Billing Dashboard** của bạn vào ngày hôm sau để đảm bảo không còn tài nguyên nào đang hoạt động.
