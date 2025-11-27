---
title : "Tạo EC2 instance"
date : "2025-10-27"
weight : 3
chapter : false
pre : " <b> 5.3 </b> "
---

#### Tạo Amazon EC2 Instance

\*\*ℹ️ Information\*\*: Amazon Elastic Compute Cloud (EC2) cung cấp khả năng tính toán có thể điều chỉnh quy mô trong đám mây AWS. Sử dụng EC2 cho phép bạn triển khai các máy chủ ảo mà không cần đầu tư vào phần cứng vật lý, giúp bạn phát triển và triển khai ứng dụng nhanh hơn.

#### Các bước tạo EC2 Instance

1. Truy cập AWS Management Console

   - Mở trình duyệt và truy cập vào Amazon EC2 console tại [https://console.aws.amazon.com/ec2/](https://console.aws.amazon.com/ec2/).

2. Khởi tạo EC2 Instance

   - Tại màn hình dashboard của EC2 console, trong hộp **Launch instance**, chọn **Launch instance**, sau đó chọn **Launch instance** từ các tùy chọn xuất hiện.

   ![Khởi tạo EC2 Instance](/images/3/0001.png?featherlight=false&width=90pc)

3. Đặt tên cho instance

   - Dưới phần **Name and tags**, cho **Name**, nhập tên mô tả cho instance của bạn.

   ![Đặt tên cho instance](/images/3/0002.png?featherlight=false&width=90pc)

4. Chọn Amazon Machine Image (AMI)

   - Dưới phần **Application and OS Images (Amazon Machine Image)**, làm theo các bước sau đây:
     - Chọn **Quick Start**, sau đó chọn **Amazon Linux**.
     - Từ **Amazon Machine Image (AMI)**, chọn một phiên bản HVM của **Amazon Linux 2023**.

   **💡 Pro Tip**: Lựa chọn AMI được đánh dấu **Free tier eligible** để tận dụng lợi ích của AWS Free Tier nếu tài khoản của bạn đủ điều kiện.

   ![Chọn AMI](/images/3/0003.png?featherlight=false&width=90pc)

5. Chọn loại instance

   - Dưới phần **Instance type**, chọn loại instance **t2.micro** hoặc **t3.micro** (trong các khu vực không có t2.micro).
   
   \*\*ℹ️ Information\*\*: Loại instance t2.micro và t3.micro đủ điều kiện sử dụng trong AWS Free Tier, phù hợp cho các ứng dụng có yêu cầu tài nguyên thấp hoặc môi trường phát triển.

   ![Chọn loại instance](/images/3/0004.png?featherlight=false&width=90pc)

6. Cấu hình key pair

   - Dưới phần **Key pair (login)**, chọn key pair mà bạn đã tạo trước đó.
   
   \*\*⚠️ Warning\*\*: Không nên chọn **Proceed without a key pair**. Nếu không có key pair, bạn sẽ không thể kết nối SSH vào instance sau khi khởi tạo.

   ![Chọn key pair](/images/3/0005.png?featherlight=false&width=90pc)

7. Cấu hình Security Group

   - Bên cạnh **Network settings**, chọn **Edit**.
   - Chọn **Select existing security group**.
   - Từ **Common security groups**, chọn security group mà bạn đã tạo trước đó.

   **🔒 Security Note**: Security Group hoạt động như tường lửa ảo, kiểm soát lưu lượng mạng đến và đi từ EC2 instance. Đảm bảo chỉ mở các cổng cần thiết để giảm thiểu bề mặt tấn công.

   ![Chọn Network Settings](/images/3/0006.png?featherlight=false&width=90pc)

   ![Chọn Security Group](/images/3/0007.png?featherlight=false&width=90pc)

8. Xác nhận và khởi tạo instance

   - Xem lại cấu hình instance trong **Summary panel**.
   - Khi đã sẵn sàng, chọn **Launch instance**.

   ![Khởi tạo instance](/images/3/0008.png?featherlight=false&width=90pc)

9. Xác nhận và kiểm tra trạng thái

   - Sau khi nhận thông báo xác nhận, chọn **View all instances** để quay lại giao diện console.
   - Theo dõi trạng thái khởi tạo instance. Ban đầu, trạng thái sẽ là **pending** và sau đó chuyển sang **running** khi instance đã sẵn sàng.
   - Đợi cho đến khi instance vượt qua kiểm tra trạng thái (Status check) trước khi thử kết nối.

   **💡 Pro Tip**: Để xem DNS công khai của instance, hãy đảm bảo cột **Public IPv4 DNS** được hiển thị bằng cách nhấp vào biểu tượng cài đặt ở góc trên bên phải.

   ![Xem danh sách instance](/images/3/0009.png?featherlight=false&width=90pc)

   ![Kiểm tra trạng thái instance](/images/3/00010.png?featherlight=false&width=90pc)

#### Kết nối vào EC2 Instance bằng SSH sử dụng MobaXterm

\*\*ℹ️ Information\*\*: MobaXterm là một ứng dụng đa năng cho Windows cung cấp nhiều công cụ mạng trong một giao diện duy nhất, bao gồm SSH client, SFTP, X11 server và nhiều tính năng khác.

1. **Tải và cài đặt MobaXterm**

   - Tải MobaXterm từ trang web chính thức: [MobaXterm Website](https://mobaxterm.mobatek.net/download-home-edition.html).
   - Cài đặt ứng dụng theo hướng dẫn.

2. **Tạo phiên SSH mới**

   - Khởi động MobaXterm.
   - Nhấp vào biểu tượng **Session** ở góc trên bên trái.

3. **Cấu hình kết nối SSH**

   - Trong cửa sổ cấu hình, điền các thông tin sau:
     - **Remote Host**: Địa chỉ IP công khai hoặc DNS công khai của EC2 instance.
     - **Port**: 22 (cổng SSH mặc định).
     - **User**: Tên người dùng mặc định (thường là **ec2-user** cho Amazon Linux).
     - **Advanced SSH settings**: Chọn tab này để cung cấp đường dẫn đến tệp khóa riêng tư (private key).

   **🔒 Security Note**: Đảm bảo tệp khóa riêng tư (.pem) của bạn có quyền truy cập hạn chế (chỉ người dùng hiện tại có thể đọc) để tăng cường bảo mật.

   ![Cấu hình kết nối SSH](/images/3/00011.png?featherlight=false&width=90pc)

4. **Kết nối vào EC2 Instance**

   - Nhấp vào **OK** để lưu cấu hình và bắt đầu phiên SSH.
   - Nếu đây là lần đầu tiên kết nối, bạn có thể nhận được cảnh báo về khóa máy chủ không xác định. Chọn **Yes** để tiếp tục.

5. **Xác nhận kết nối thành công**

   - Sau khi kết nối thành công, bạn sẽ thấy terminal của EC2 instance và có thể bắt đầu thực hiện các lệnh.

   **💡 Pro Tip**: MobaXterm tự động lưu các phiên làm việc gần đây, giúp bạn dễ dàng kết nối lại vào các instance thường xuyên sử dụng mà không cần cấu hình lại.

   ![Kết nối SSH thành công](/images/3/00012.png?featherlight=false&width=90pc)

