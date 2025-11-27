---
title : "Dọn dẹp tài nguyên"
date : "2025-10-27"
weight : 7
chapter : false
pre : " <b> 5.7 </b> "
---

#### Dọn dẹp Tài nguyên

**ℹ️ Information**: Để tránh các chi phí không mong muốn, việc dọn dẹp tất cả các tài nguyên đã tạo trong workshop này là rất quan trọng. Chúng ta sẽ xóa các tài nguyên theo thứ tự ngược lại với quy trình tạo.

#### Bước 1: Xóa Tài nguyên RDS

1.  **Xóa RDS Instance**:
    -   Truy cập console **Amazon RDS** > **Databases**.
    -   Chọn database instance của bạn (ví dụ: `workshop-db`).
    -   Nhấp **Actions** > **Delete**.
    -   Bỏ chọn **Create final snapshot** và đánh dấu vào ô **I acknowledge...**.
    -   Nhập `delete me` và nhấp **Delete**.

2.  **Xóa DB Subnet Group**:
    -   Đi tới **Subnet groups**.
    -   Chọn nhóm của bạn (ví dụ: `rds-subnet-group`).
    -   Nhấp **Delete**.

#### Bước 2: Terminate EC2 Instance

1.  **Terminate Instance**:
    -   Truy cập console **Amazon EC2** > **Instances**.
    -   Chọn instance của bạn (ví dụ: `Workshop-Web-Server`).
    -   Nhấp **Instance state** > **Terminate instance**.
    -   Nhấp **Terminate**.

#### Bước 3: Xóa Tài nguyên Mạng

1.  **Xóa Security Groups**:
    -   Truy cập console **VPC** > **Security Groups**.
    -   Chọn **RDS Security Group** và xóa nó.
    -   Chọn **EC2 Security Group** và xóa nó.

    **💡 Pro Tip**: Bạn phải xóa RDS Security Group trước vì EC2 Security Group có thể đang tham chiếu đến nó (hoặc ngược lại tùy thuộc vào quy tắc của bạn). Nếu gặp lỗi phụ thuộc, hãy kiểm tra các quy tắc Inbound/Outbound.

2.  **Xóa VPC**:
    -   Đi tới **Your VPCs**.
    -   Chọn VPC workshop của bạn.
    -   Nhấp **Actions** > **Delete VPC**.
    -   Nhập `delete` và xác nhận.

    **ℹ️ Information**: Xóa VPC sẽ tự động xóa các subnet, bảng định tuyến và internet gateway liên quan.

#### Xác minh

1.  Kiểm tra **Billing Dashboard** của bạn vào ngày hôm sau để đảm bảo không còn tài nguyên nào đang hoạt động.
