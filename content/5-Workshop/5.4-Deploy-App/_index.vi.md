---
title: "Triển khai Ứng dụng"
date: "2025-10-27"
weight: 4
chapter: false
pre: " <b> 5.4 </b> "
---

# Triển khai Ứng dụng

Sau khi cơ sở hạ tầng đã sẵn sàng (Network, Database, IAM), chúng ta có thể tiến hành triển khai các thành phần ứng dụng.

Chúng ta sẽ chia phần này thành hai phần:
1.  **Triển khai Backend**: Container hóa ứng dụng Spring Boot, đẩy lên ECR và chạy an toàn trên AWS Lambda với API Gateway.
2.  **Triển khai Frontend**: Lưu trữ React SPA trên S3 và phân phối toàn cầu qua CloudFront.

Hãy bắt đầu với Backend.
