---
title : "Tạo EC2 Security Group"
date : "2025-10-27"
weight : 2
chapter : false
pre : " <b> 5.2.2 </b> "
---

#### Tạo Security Group cho Amazon EC2

**ℹ️ Information**: Security Group hoạt động như một tường lửa ảo cho các EC2 instance của bạn để kiểm soát lưu lượng truy cập đến và đi. Trong bước này, chúng ta sẽ tạo một security group cho phép truy cập vào ứng dụng web của chúng ta.

#### Hướng dẫn từng bước

1.  Điều hướng đến **EC2 Dashboard** trong AWS Management Console.

2.  Trong thanh điều hướng bên trái, dưới mục **Network & Security**, chọn **Security Groups**.

3.  Nhấn **Create security group**.

    ![Create a Security Group](/images/1/0009.png?featherlight=false&width=90pc)

4.  **Basic details**:
    - **Security group name**: Nhập tên mô tả (ví dụ: `EC2-Web-SG`).
    - **Description**: Nhập mô tả (ví dụ: `Allow Web and SSH access`).
    - **VPC**: Chọn VPC bạn đã tạo ở bước trước.

    ![Configure Security Group Details](/images/1/00010.png?featherlight=false&width=90pc)

5.  **Inbound rules**: Nhấn **Add rule** để cho phép các lưu lượng sau:

    | Loại | Giao thức | Dải cổng | Nguồn | Mô tả |
    | :--- | :--- | :--- | :--- | :--- |
    | **HTTP** | TCP | 80 | 0.0.0.0/0 | Cho phép truy cập HTTP từ mọi nơi |
    | **HTTPS** | TCP | 443 | 0.0.0.0/0 | Cho phép truy cập HTTPS từ mọi nơi |
    | **Custom TCP** | TCP | 5000 | 0.0.0.0/0 | Cho phép truy cập cổng ứng dụng |
    | **SSH** | TCP | 22 | My IP | Chỉ cho phép truy cập SSH từ IP của bạn |

    **🔒 Security Note**: Đối với SSH (Cổng 22), luôn chọn **My IP** làm nguồn để giới hạn quyền truy cập quản trị chỉ từ vị trí hiện tại của bạn. Không bao giờ mở SSH cho `0.0.0.0/0` trong môi trường sản xuất.

    ![Configure Inbound Rules](/images/1/00011.png?featherlight=false&width=90pc)

6.  **Outbound rules**: Giữ nguyên quy tắc mặc định (Cho phép tất cả lưu lượng).

7.  Nhấn **Create security group**.

    ![Create the Security Group](/images/1/00012.png?featherlight=false&width=90pc)

8.  Ghi lại **Security Group ID** (ví dụ: `sg-xxxxxxxx`), vì bạn sẽ cần nó sau này.

    ![Security Group Created](/images/1/00013.png?featherlight=false&width=90pc)

**💡 Pro Tip**: Security Group có tính **stateful**. Điều này có nghĩa là nếu bạn cho phép một yêu cầu đi vào (inbound), phản hồi sẽ tự động được phép đi ra (outbound), bất kể quy tắc outbound là gì.
