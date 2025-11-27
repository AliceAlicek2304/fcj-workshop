---
title : "Tạo DB Subnet Group"
date : "2025-10-27"
weight : 4
chapter : false
pre : " <b> 5.2.4 </b> "
---

#### Tạo DB Subnet Group cho Amazon RDS

**ℹ️ Information**: Một **DB Subnet Group** là tập hợp các subnet (thường là private) mà bạn chỉ định cho các RDS instance của mình. Nó cho RDS biết những subnet và dải IP nào có thể sử dụng trong VPC của bạn.

**⚠️ Warning**: Để kích hoạt triển khai Multi-AZ (Tính sẵn sàng cao), DB Subnet Group của bạn **phải** bao gồm các subnet trong ít nhất **hai Availability Zone khác nhau**.

#### Hướng dẫn từng bước

1.  Điều hướng đến bảng điều khiển **Amazon RDS**.

2.  Trong thanh điều hướng bên trái, chọn **Subnet groups**.

3.  Nhấn **Create DB Subnet Group**.

    ![Create DB Subnet Group](/images/2/0005.png?featherlight=false&width=90pc)

4.  **Subnet group details**:
    - **Name**: Nhập tên (ví dụ: `rds-subnet-group`).
    - **Description**: Nhập mô tả (ví dụ: `Subnet group for RDS`).
    - **VPC**: Chọn VPC của bạn.

    ![Configure DB Subnet Group Details](/images/2/0006.png?featherlight=false&width=90pc)

5.  **Add subnets**:
    - **Availability Zones**: Chọn các Availability Zone nơi bạn đã tạo các private subnet (ví dụ: `us-east-1a` và `us-east-1b`).
    - **Subnets**: Chọn các **Private Subnet ID** cụ thể liên kết với các AZ đó.

    **🔒 Security Note**: Luôn chọn **Private Subnets** cho cơ sở dữ liệu của bạn để đảm bảo nó không thể truy cập trực tiếp từ internet.

6.  Nhấn **Create**.

    ![Add Subnets to DB Subnet Group](/images/2/0007.png?featherlight=false&width=90pc)

7.  DB Subnet Group của bạn hiện đã sẵn sàng.

    ![DB Subnet Group Created](/images/2/0008.png?featherlight=false&width=90pc)

**💡 Pro Tip**: Nếu bạn đang sử dụng AWS Local Zones, bạn cũng có thể bao gồm chúng ở đây để mở rộng cơ sở dữ liệu của bạn đến gần hơn với người dùng cuối.
