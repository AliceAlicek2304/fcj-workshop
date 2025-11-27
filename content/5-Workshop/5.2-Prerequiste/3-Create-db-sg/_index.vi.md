---
title : "Tạo RDS Security Group"
date : "2025-10-27"
weight : 3
chapter : false
pre : " <b> 5.2.3 </b> "
---

#### Tạo Security Group cho Amazon RDS

**ℹ️ Information**: Giống như EC2 instance, cơ sở dữ liệu RDS của chúng ta cũng cần một Security Group để kiểm soát lưu lượng truy cập. Security group này sẽ hoạt động như một bức tường lửa, **chỉ** cho phép truy cập từ các máy chủ ứng dụng của chúng ta.

#### Hướng dẫn từng bước

1.  Trong **VPC Dashboard**, chọn **Security Groups** từ thanh điều hướng bên trái.

2.  Nhấn **Create security group**.

    ![Create a Security Group](/images/2/0001.png?featherlight=false&width=90pc)

3.  **Basic details**:
    - **Security group name**: Nhập tên mô tả (ví dụ: `RDS-MySQL-SG`).
    - **Description**: Nhập mô tả (ví dụ: `Allow MySQL access from EC2`).
    - **VPC**: Chọn VPC tương tự như bước trước.

4.  **Inbound rules**: Nhấn **Add rule** để cho phép kết nối cơ sở dữ liệu:

    | Loại | Giao thức | Dải cổng | Nguồn | Mô tả |
    | :--- | :--- | :--- | :--- | :--- |
    | **MySQL/Aurora** | TCP | 3306 | **sg-xxxxxxxx** (EC2-Web-SG) | Cho phép truy cập MySQL từ EC2 SG |

    **🔒 Security Note**: Thay vì nhập địa chỉ IP (như `0.0.0.0/0`), hãy chọn **Security Group ID** của EC2 Security Group mà bạn đã tạo ở bước trước. Điều này đảm bảo rằng **chỉ** các instance thuộc về security group cụ thể đó mới có thể kết nối với cơ sở dữ liệu của bạn. Đây là một thực hành tốt nhất về bảo mật.

    ![Configure Inbound Rules](/images/2/0002.png?featherlight=false&width=90pc)

5.  **Outbound rules**: Giữ nguyên quy tắc mặc định (Cho phép tất cả lưu lượng).

6.  Nhấn **Create security group**.

    ![Create the Security Group](/images/2/0003.png?featherlight=false&width=90pc)

7.  Bây giờ bạn đã có một security group dành riêng cho lớp cơ sở dữ liệu của mình.

    ![Security Group Created](/images/2/0004.png?featherlight=false&width=90pc)

**⚠️ Warning**: Không bao giờ sử dụng cùng một Security Group cho cả EC2 instance và RDS instance của bạn. Việc phân tách nhiệm vụ là chìa khóa cho một kiến trúc an toàn.
