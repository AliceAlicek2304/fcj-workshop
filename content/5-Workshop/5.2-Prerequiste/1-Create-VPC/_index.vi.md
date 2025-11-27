---
title : "Tạo VPC"
date : "2025-10-27"
weight : 1
chapter : false
pre : " <b> 5.2.1 </b> "
---

#### Tạo VPC với Subnets và các tài nguyên liên quan

**ℹ️ Information**: Amazon Virtual Private Cloud (Amazon VPC) là mạng riêng của bạn trên đám mây. Nó cho phép bạn khởi chạy các tài nguyên AWS vào một mạng ảo do bạn định nghĩa, mang lại cho bạn quyền kiểm soát hoàn toàn đối với môi trường mạng của mình.

Chúng ta sẽ sử dụng trình hướng dẫn **VPC and more** để tạo VPC, subnets, bảng định tuyến (route tables) và cổng internet (internet gateway) trong một quy trình duy nhất.

#### Hướng dẫn từng bước

1.  Mở bảng điều khiển Amazon VPC tại [https://console.aws.amazon.com/vpc/](https://console.aws.amazon.com/vpc/).

    ![Create a VPC](/images/1/0001.png?featherlight=false&width=90pc)

2.  Trên bảng điều khiển VPC, chọn **Create VPC**.

3.  Trong phần **Resources to create**, chọn **VPC and more**. Tùy chọn này sẽ tự động cung cấp các tài nguyên liên quan như subnet và bảng định tuyến.

    ![Create a VPC](/images/1/0002.png?featherlight=false&width=90pc)

4.  **Name tag auto-generation**: Nhập tên cho dự án của bạn (ví dụ: `workshop-vpc`). Tên này sẽ được sử dụng làm tiền tố cho tất cả các tài nguyên được tạo.

5.  **IPv4 CIDR block**: Giữ nguyên mặc định (ví dụ: `10.0.0.0/16`) hoặc nhập dải IP bạn muốn.

6.  **Availability Zones (AZs)**: Chọn **2**. Điều này rất quan trọng cho Tính sẵn sàng cao (High Availability) và triển khai Multi-AZ.

    ![Create a VPC](/images/1/0003.png?featherlight=false&width=90pc)

7.  **Number of public subnets**: Chọn **2**. Các subnet này sẽ chứa các tài nguyên cần truy cập internet trực tiếp (như bastion host hoặc load balancer).

8.  **Number of private subnets**: Chọn **2**. Các subnet này sẽ chứa các instance cơ sở dữ liệu RDS của bạn, giữ chúng an toàn khỏi internet công cộng.

    **🔒 Security Note**: Luôn đặt các instance cơ sở dữ liệu của bạn trong các private subnet.

9.  **NAT gateways**: Chọn **1 per AZ** hoặc **1 in 1 AZ** tùy thuộc vào ngân sách của bạn. Đối với workshop này, **None** hoặc **1 in 1 AZ** là đủ nếu bạn cần truy cập internet chiều đi cho các private instance (ví dụ: để cập nhật).

    **💡 Pro Tip**: Trong môi trường sản xuất, việc triển khai NAT Gateway trong mỗi AZ đảm bảo tính sẵn sàng cao nhưng sẽ phát sinh chi phí cao hơn.

10. **VPC endpoints**: Để là **None** cho workshop này.

11. **DNS options**: Đảm bảo **Enable DNS hostnames** và **Enable DNS resolution** được chọn. Các tùy chọn này là cần thiết để RDS hoạt động chính xác với truy cập công khai (nếu cần) và để phân giải tên miền nội bộ dễ dàng hơn.

12. Xem lại bảng **Preview** để hình dung kiến trúc mạng của bạn.

13. Nhấn **Create VPC**.

    ![Create a VPC](/images/1/0004.png?featherlight=false&width=90pc)

    ![Create a VPC](/images/1/0005.png?featherlight=false&width=90pc)

#### Cấu hình gán IP công khai (Tùy chọn)

**ℹ️ Information**: Theo mặc định, các instance trong subnet không mặc định sẽ không nhận được địa chỉ IP công khai. Nếu bạn muốn các instance trong **Public Subnets** của mình tự động nhận IP công khai, hãy làm theo các bước sau:

1.  Đi tới **Subnets** trong thanh điều hướng bên trái.
2.  Chọn một trong các **Public Subnets** của bạn.
3.  Nhấn **Actions** > **Edit subnet settings**.

    ![Create a VPC](/images/1/0007.png?featherlight=false&width=90pc)

4.  Đánh dấu chọn **Enable auto-assign public IPv4 address**.
5.  Nhấn **Save**.
6.  Lặp lại cho Public Subnet còn lại của bạn.

    ![Create a VPC](/images/1/0008.png?featherlight=false&width=90pc)

**⚠️ Warning**: Không bao giờ bật tự động gán IP công khai cho **Private Subnets** nơi chứa cơ sở dữ liệu của bạn.
