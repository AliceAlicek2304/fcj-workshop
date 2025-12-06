---
title: "Workshop: Triển khai GameTracker lên AWS"
date: "2025-10-27"
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Workshop: Triển khai GameTracker lên AWS

## Tổng quan

Chào mừng bạn đến với **GameTracker Deployment Workshop**. Trong buổi thực hành này, bạn sẽ học cách triển khai một ứng dụng web 3 lớp hoàn chỉnh lên AWS sử dụng các công nghệ hiện đại.

Bạn sẽ chuyển đổi từ môi trường phát triển local sang kiến trúc cloud sẵn sàng cho production.

### Bạn sẽ xây dựng gì?

Bạn sẽ triển khai **GameTracker**, một ứng dụng web theo dõi chỉ số người chơi. Kiến trúc bao gồm:
-   **Frontend**: React Single Page Application (SPA) được lưu trữ trên **Amazon S3** và phân phối qua **Amazon CloudFront**.
-   **Backend**: Spring Boot REST API được đóng gói Docker, chạy trên **AWS Lambda** (Serverless).
-   **Database**: **Amazon RDS cho SQL Server** để lưu trữ dữ liệu game.
-   **Network**: Một **VPC** tùy chỉnh với các public/private subnet và security groups.

![Architecture](/images/1/0001.png?featherlight=false&width=90pc)

## Cấu trúc Workshop

Workshop này được chia thành các mô-đun sau:

1.  **[Giới thiệu](5.1-introduce/)**: Tổng quan dự án, kiến trúc và các dịch vụ AWS sử dụng.
2.  **[Chuẩn bị](5.2-prerequiste/)**: Thiết lập nền tảng (VPC, IAM, Security Groups, NAT Gateway).
3.  **[Tạo Database](5.3-create-rds/)**: Khởi tạo Amazon RDS SQL Server instance.
4.  **[Triển khai Ứng dụng](5.4-deploy-app/)**:
    -   Đóng gói và deploy Backend (ECR, Lambda, API Gateway).
    -   Host và phân phối Frontend (S3, CloudFront).
5.  **[Sao lưu & Phục hồi](6-backup/)**: Chiến lược bảo vệ dữ liệu.
6.  **[Dọn dẹp](7-cleanup/)**: Xóa tài nguyên để tránh phát sinh chi phí.

## Yêu cầu tiên quyết

Trước khi bắt đầu, hãy đảm bảo bạn có:
-   Một **AWS Account** đang hoạt động.
-   **AWS CLI** đã được cài đặt và cấu hình.
-   **Docker** đã cài đặt trên máy.
-   **Java 17+** và **Node.js** (để build ứng dụng).

Hãy bắt đầu nào!
