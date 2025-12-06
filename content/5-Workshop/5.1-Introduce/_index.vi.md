---
title: "Giới thiệu"
date: "2025-10-27"
weight: 1 
chapter: false
pre: " <b> 5.1 </b> "
---

# Triển khai GameTracker trên AWS

## 🎯 Mục tiêu Workshop
Trong workshop này, chúng ta sẽ thực hành triển khai nền tảng **GameTracker**—một ứng dụng web full-stack—lên AWS hoàn toàn từ đầu. Bạn sẽ xây dựng một kiến trúc serverless tiêu chuẩn sử dụng các dịch vụ phổ biến trong ngành.

Mục tiêu là tạo ra một môi trường giống production tại region **Sydney (ap-southeast-2)**, bao gồm mọi thứ từ thiết lập mạng (networking) đến triển khai ứng dụng.

## 🏗️ Tổng quan Kiến trúc

Giải pháp áp dụng kiến trúc cloud-native hiện đại:
- **Frontend**: Ứng dụng React Single Page Application (SPA) được lưu trữ trên **Amazon S3** và phân phối qua **Amazon CloudFront**.
- **Backend**: Ứng dụng Spring Boot được đóng gói container với Docker, lưu trữ trong **Amazon ECR**, và chạy dưới dạng serverless trên **AWS Lambda**, được public thông qua **API Gateway**.
- **Database**: **SQL Server Express** chạy trên **Amazon RDS** để quản lý dữ liệu game có cấu trúc.
- **Mạng**: Một **VPC** tùy chỉnh với các subnet public/private và security group để đảm bảo sự cô lập và bảo mật.

![Architecture](/images/2-Proposal/GameTracker1.jpg)

## 📋 Các dịch vụ sử dụng
Chúng ta sẽ cấu hình các dịch vụ AWS sau:

| Danh mục | Dịch vụ |
|----------|----------|
| **Networking** | VPC, Subnets, Internet Gateway, NAT Gateway (tùy chọn), Route53 |
| **Compute** | AWS Lambda, API Gateway (HTTP API) |
| **Storage** | Amazon S3 (Frontend & Assets) |
| **Database** | Amazon RDS (SQL Server) |
| **Container** | Amazon ECR (Elastic Container Registry) |
| **CDN & Security** | Amazon CloudFront, AWS WAF, IAM, Security Groups |

## 🚀 Các bước triển khai
Workshop này được chia thành các giai đoạn logic:

1.  **Thiết lập Mạng**: Tạo VPC, Subnets, và Routing.
2.  **Cung cấp Cơ sở dữ liệu**: Thiết lập RDS SQL Server.
3.  **Triển khai Backend**:
    - Tạo ECR Repository.
    - Build và push Docker image.
    - Tạo Lambda function và kết nối với database.
    - Public backend thông qua API Gateway.
4.  **Triển khai Frontend**:
    - Tạo S3 buckets.
    - Thiết lập CloudFront distribution.
    - Deploy ứng dụng React.
5.  **Dọn dẹp**: Hướng dẫn xóa tài nguyên để tránh phát sinh chi phí.

## 🛠️ Điều kiện tiên quyết

Trước khi bắt đầu, hãy đảm bảo bạn có:

1.  **AWS Account**: Tài khoản hoạt động với quyền admin.
2.  **Công cụ cài đặt**:
    -   [AWS CLI](https://aws.amazon.com/cli/) (Đã cấu hình với `aws configure`).
    -   [Docker Desktop](https://www.docker.com/products/docker-desktop/).
    -   [Node.js](https://nodejs.org/) và [Java 17](https://adoptium.net/).
3.  **Mã nguồn (Source Code)**:
    -   Clone repository của workshop:
        ```bash
        git clone https://github.com/your-repo/gametracker-workshop.git
        cd gametracker-workshop
        ```

---

**Lưu ý**: Một số tài nguyên như **RDS** và **NAT Gateway** tính phí theo giờ. Vui lòng làm theo phần **Dọn dẹp (Cleanup)** ngay sau khi hoàn thành workshop để tránh các khoản phí không mong muốn.
