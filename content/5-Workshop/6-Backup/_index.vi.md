---
title : "Backup và restore"
date : "2025-10-27"
weight : 6
chapter : false
pre : " <b> 5.6 </b> "
---

#### Backup và Restore trong Amazon RDS

\*\*ℹ️ Information\*\*: Amazon RDS cung cấp các tính năng backup tự động và thủ công, cho phép bạn khôi phục cơ sở dữ liệu về một thời điểm cụ thể hoặc từ một snapshot. Việc này giúp bảo vệ dữ liệu của bạn khỏi mất mát và đảm bảo tính liên tục của ứng dụng.

#### Giám sát Amazon RDS

1. Truy cập trang giám sát hiệu suất của RDS instance:

   - Đăng nhập vào AWS Management Console
   - Chọn dịch vụ **Amazon RDS**
   - Trong bảng điều khiển, chọn **Databases**
   - Chọn DB instance mà bạn muốn giám sát
   - Chọn tab **Monitoring**

   ![Giao diện giám sát RDS](/images/5/00014.png?featherlight=false&width=90pc)
   ![Biểu đồ CPU Utilization](/images/5/00015.png?featherlight=false&width=90pc)
   ![Biểu đồ Database Connections](/images/5/00016.png?featherlight=false&width=90pc)
   ![Biểu đồ Free Storage Space](/images/5/00017.png?featherlight=false&width=90pc)
   ![Biểu đồ Read/Write IOPS](/images/5/00018.png?featherlight=false&width=90pc)

   **💡 Pro Tip**: Thiết lập CloudWatch Alarms cho các metric quan trọng như CPU Utilization, Free Storage Space, và Database Connections để nhận thông báo khi các giá trị vượt ngưỡng.

#### Quản lý Backup trong Amazon RDS

2. Xem thông tin backup của DB instance:

   - Trong bảng điều khiển Amazon RDS, chọn DB instance của bạn
   - Chuyển đến tab **Maintenance & backups**
   - Tại đây, bạn có thể xem và quản lý cả backup tự động và thủ công

   ![Cấu hình backup RDS](/images/5/00019.png?featherlight=false&width=90pc)

   \*\*ℹ️ Information\*\*: Amazon RDS tự động tạo và lưu trữ backup hàng ngày trong khoảng thời gian lưu giữ bạn đã cấu hình (1-35 ngày). Bạn cũng có thể tạo snapshot thủ công bất kỳ lúc nào.

3. Xem danh sách DB snapshots:

   ![Danh sách DB snapshots](/images/5/00020.png?featherlight=false&width=90pc)

   **🔒 Security Note**: Snapshots của RDS được mã hóa nếu DB instance nguồn được mã hóa. Đảm bảo rằng bạn đã bật mã hóa cho các DB instance quan trọng.

#### Khôi phục từ DB Snapshot

4. Bắt đầu quá trình khôi phục snapshot:

   - Chọn DB snapshot mà bạn muốn khôi phục
   - Từ menu **Actions**, chọn **Restore snapshot**

   ![Chọn Restore snapshot](/images/5/00021.png?featherlight=false&width=90pc)

5. Cấu hình DB instance mới:

   - Nhập tên cho DB instance mới trong ô **DB instance identifier**
   - Chọn các cấu hình phù hợp như instance class, storage type và allocated storage
   - Cấu hình network settings, security groups và các tùy chọn khác
   - Chọn **Restore DB instance** để bắt đầu quá trình khôi phục

   ![Cấu hình DB instance mới](/images/5/00022.png?featherlight=false&width=90pc)
   ![Chọn instance specifications](/images/5/00023.png?featherlight=false&width=90pc)
   ![Cấu hình storage](/images/5/00024.png?featherlight=false&width=90pc)
   ![Cấu hình connectivity](/images/5/00025.png?featherlight=false&width=90pc)
   ![Xác nhận restore](/images/5/00026.png?featherlight=false&width=90pc)

   \*\*⚠️ Warning\*\*: Khi khôi phục từ snapshot, DB instance mới sẽ có tên khác với instance gốc. Đảm bảo cập nhật chuỗi kết nối trong ứng dụng của bạn để trỏ đến endpoint mới.

6. Xác nhận quá trình khôi phục đã bắt đầu:

   ![Quá trình restore đang diễn ra](/images/5/00027.png?featherlight=false&width=90pc)

7. Kiểm tra DB instance đã khôi phục:

   ![DB instance đã khôi phục thành công](/images/5/00028.png?featherlight=false&width=90pc)

   **💡 Pro Tip**: Sau khi khôi phục, hãy kiểm tra các thông số cấu hình như parameter groups, option groups và security groups để đảm bảo chúng phù hợp với yêu cầu của ứng dụng của bạn.

