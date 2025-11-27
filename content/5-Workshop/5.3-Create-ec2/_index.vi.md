---
title : "Tạo EC2 instance"
date : "2025-10-27"
weight : 3
chapter : false
pre : " <b> 5.3 </b> "
---

#### Tạo Amazon EC2 Instance

**ℹ️ Information**: Amazon EC2 (Elastic Compute Cloud) cung cấp khả năng tính toán có thể mở rộng trên đám mây AWS. Nó cho phép bạn khởi chạy các máy chủ ảo (instance) chỉ trong vài phút, loại bỏ nhu cầu đầu tư phần cứng trả trước.

Trong bước này, chúng ta sẽ khởi chạy một Linux EC2 instance đóng vai trò là máy chủ ứng dụng (hoặc bastion host) để kết nối với cơ sở dữ liệu RDS của chúng ta.

#### Hướng dẫn từng bước

1.  **Truy cập Console**: Mở [Amazon EC2 console](https://console.aws.amazon.com/ec2/).

2.  **Launch Instance**: Trên bảng điều khiển, nhấp vào nút màu cam **Launch instance**.

    ![Create a VPC](/images/3/0001.png?featherlight=false&width=90pc)

3.  **Name and Tags**:
    - **Name**: Nhập tên mô tả (ví dụ: `Workshop-Web-Server`).

    ![Create a VPC](/images/3/0002.png?featherlight=false&width=90pc)

4.  **Application and OS Images (AMI)**:
    - **Quick Start**: Chọn **Amazon Linux**.
    - **AMI**: Chọn **Amazon Linux 2023 AMI** (Free tier eligible).

    **💡 Pro Tip**: Luôn tìm thẻ "Free tier eligible" để tránh các chi phí không mong muốn trong quá trình học tập hoặc thử nghiệm.

    ![Create a VPC](/images/3/0003.png?featherlight=false&width=90pc)

5.  **Instance Type**:
    - Chọn **t2.micro** (hoặc **t3.micro** nếu t2 không có sẵn trong khu vực của bạn).

    **ℹ️ Information**: Các loại instance này có chi phí thấp và thường được bao gồm trong AWS Free Tier.

    ![Create a VPC](/images/3/0004.png?featherlight=false&width=90pc)

6.  **Key Pair (Login)**:
    - Chọn **Key pair** bạn đã tạo trước đó.

    **⚠️ Warning**: Không tiếp tục nếu không có key pair. Bạn sẽ không thể SSH vào instance của mình nếu thiếu nó.

    ![Create a VPC](/images/3/0005.png?featherlight=false&width=90pc)

7.  **Network Settings**:
    - Nhấp vào **Edit**.
    - **VPC**: Chọn VPC workshop của bạn.
    - **Subnet**: Chọn một **Public Subnet**.
    - **Auto-assign Public IP**: Đảm bảo tùy chọn này là **Enabled**.
    - **Firewall (security groups)**: Chọn **Select existing security group**.
    - Chọn **EC2 Security Group** bạn đã tạo ở bước 5.2.2.

    **🔒 Security Note**: Bằng cách tái sử dụng security group chúng ta đã tạo trước đó, chúng ta đảm bảo instance có chính xác các quyền cần thiết—không thừa, không thiếu.

    ![Create a VPC](/images/3/0006.png?featherlight=false&width=90pc)
    ![Create a VPC](/images/3/0007.png?featherlight=false&width=90pc)

8.  **Launch**:
    - Xem lại tóm tắt cấu hình.
    - Nhấp vào **Launch instance**.

    ![Create a VPC](/images/3/0008.png?featherlight=false&width=90pc)

9.  **Xác minh**:
    - Nhấp vào **View all instances**.
    - Đợi cho đến khi **Instance state** chuyển sang `Running` và **Status check** báo thành công.

    **💡 Pro Tip**: Nếu bạn không thấy cột Public DNS, hãy nhấp vào biểu tượng bánh răng cài đặt và bật **Public IPv4 DNS**.

    ![Create a VPC](/images/3/0009.png?featherlight=false&width=90pc)
    ![Create a VPC](/images/3/00010.png?featherlight=false&width=90pc)

#### Kết nối qua SSH (MobaXterm)

**ℹ️ Information**: MobaXterm là một terminal mạnh mẽ cho Windows giúp việc kết nối SSH trở nên dễ dàng.

1.  **Tải xuống & Cài đặt**: Tải MobaXterm từ [trang web chính thức](https://mobaxterm.mobatek.net/download-home-edition.html).

2.  **Tạo phiên kết nối (Session)**:
    - Nhấp vào **Session** > **SSH**.
    - **Remote host**: Nhập **Public IPv4 DNS** của EC2 instance.
    - **Specify username**: Nhập `ec2-user`.
    - **Port**: `22`.

3.  **Xác thực**:
    - Chuyển đến tab **Advanced SSH settings**.
    - Đánh dấu chọn **Use private key**.
    - Duyệt và chọn tệp khóa `.pem` của bạn.

    ![Create a VPC](/images/3/00011.png?featherlight=false&width=90pc)

4.  **Kết nối**:
    - Nhấp vào **OK**.
    - Bạn sẽ được kết nối với máy chủ Linux của mình!

    ![Create a VPC](/images/3/00012.png?featherlight=false&width=90pc)

**🔒 Security Note**: Giữ an toàn cho tệp khóa `.pem` của bạn. Không bao giờ chia sẻ nó hoặc đưa nó lên các kho lưu trữ công khai.
