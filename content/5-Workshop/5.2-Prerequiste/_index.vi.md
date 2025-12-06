---
title: "Chuẩn bị"
date: "2025-10-27"
weight: 2
chapter: false
pre: " <b> 5.2 </b> "
---

# Các bước chuẩn bị

Trước khi triển khai ứng dụng GameTracker, chúng ta cần thiết lập cơ sở hạ tầng nền tảng. Điều này bao gồm lớp mạng (VPC), cấu hình bảo mật (IAM Roles, Security Groups) và các quyền cần thiết.

Trong phần này, chúng ta sẽ:
1.  **Tạo Hạ tầng Mạng**: VPC, Subnets, Internet Gateway, và Route Tables.
2.  **Tạo IAM Roles**: Các role thực thi cho AWS Lambda.
3.  **Tạo Security Groups**: Các quy tắc tường lửa cho các thành phần của hệ thống.

Các bước này đảm bảo một môi trường an toàn và cô lập cho ứng dụng.
