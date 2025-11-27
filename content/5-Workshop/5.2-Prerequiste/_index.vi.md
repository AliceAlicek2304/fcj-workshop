---
title : "Các bước chuẩn bị"
date : "2025-10-27"
weight : 2 
chapter : false
pre : " <b> 5.2 </b> "
---

#### Tổng quan

**ℹ️ Information**: Trước khi có thể khởi chạy cơ sở dữ liệu Amazon RDS, chúng ta cần xây dựng nền móng vững chắc. Điều này bao gồm việc thiết lập hạ tầng mạng an toàn và mạnh mẽ trong môi trường AWS của bạn.

Trong phần này, chúng ta sẽ lần lượt tạo các thành phần thiết yếu sau:

1.  **Virtual Private Cloud (VPC)**: Môi trường mạng biệt lập cho các tài nguyên của bạn.
2.  **Subnets**: Các phân đoạn mạng được phân phối trên nhiều Availability Zones để đảm bảo tính sẵn sàng cao.
3.  **Security Groups**: Tường lửa ảo để kiểm soát lưu lượng truy cập cho cả ứng dụng (EC2) và cơ sở dữ liệu (RDS) của bạn.
4.  **DB Subnet Group**: Một tập hợp các subnet cho RDS biết nơi nó có thể cung cấp các instance cơ sở dữ liệu.

#### Tại sao điều này lại quan trọng?

Việc thiết lập chính xác các thành phần này là rất quan trọng để:
- **Bảo mật**: Cách ly cơ sở dữ liệu của bạn khỏi truy cập công khai từ internet.
- **Tính sẵn sàng**: Đảm bảo cơ sở dữ liệu có thể tồn tại ngay cả khi trung tâm dữ liệu gặp sự cố (Multi-AZ).
- **Khả năng kết nối**: Cho phép các máy chủ ứng dụng giao tiếp an toàn với cơ sở dữ liệu.

**💡 Pro Tip**: Luôn thiết kế mạng của bạn với tư duy hướng đến **Tính sẵn sàng cao (High Availability)**. Bằng cách tạo subnet trong ít nhất hai Availability Zone khác nhau ngay bây giờ, bạn sẽ kích hoạt được tùy chọn triển khai Multi-AZ sau này.

**🔒 Security Note**: Chúng ta sẽ tuân theo nguyên tắc **Đặc quyền tối thiểu (Least Privilege)**. Các Security Group sẽ được cấu hình để chỉ cho phép lưu lượng cần thiết trên các cổng cụ thể từ các nguồn được ủy quyền.

**⚠️ Warning**: Bạn không thể tạo triển khai RDS Multi-AZ nếu DB Subnet Group của bạn không bao gồm các subnet trong ít nhất hai Availability Zone.
