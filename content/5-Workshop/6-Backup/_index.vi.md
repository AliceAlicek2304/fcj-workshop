---
title : "Backup và Restore"
date : "2025-10-27"
weight : 6
chapter : false
pre : " <b> 5.6 </b> "
---

#### Hiểu về Backup và Restore trong Amazon RDS

**ℹ️ Information**: Amazon RDS cung cấp các tính năng backup tự động và cho phép tạo snapshot thủ công để đảm bảo dữ liệu của bạn được bảo vệ và có thể khôi phục khi cần thiết. Các khả năng này là thiết yếu cho kế hoạch khôi phục sau thảm họa và duy trì tính liên tục của doanh nghiệp.

#### Giám sát Trạng thái Backup

1.  **Truy cập Giám sát**:
    -   Điều hướng đến phần **Databases** trong AWS Management Console.
    -   Chọn DB instance mục tiêu của bạn.
    -   Nhấp vào tab **Monitoring** để xem các chỉ số hiệu suất.

    ![AWS RDS Monitoring](/images/5/00014.png?featherlight=false&width=90pc)

#### Quản lý Backup

1.  **Xem Chi tiết Backup**:
    -   Chọn DB instance của bạn.
    -   Điều hướng đến tab **Maintenance & backups**.
    -   Tại đây, bạn có thể xem thông tin về cả backup tự động và thủ công, cũng như cấu hình cài đặt backup.

    ![AWS RDS Backup](/images/5/00019.png?featherlight=false&width=90pc)

2.  **Xem Snapshots**:
    -   Trong thanh điều hướng bên trái, nhấp vào **Snapshots**.
    -   Bạn sẽ thấy danh sách tất cả các snapshot thủ công và tự động.

    ![Snapshot Information](/images/5/00020.png?featherlight=false&width=90pc)

#### Khôi phục từ DB Snapshot

**ℹ️ Information**: Khôi phục một snapshot sẽ tạo ra một DB instance **mới**. Nó không ghi đè lên instance hiện có.

1.  **Chọn Snapshot**:
    -   Chọn DB snapshot bạn muốn khôi phục.
    -   Nhấp vào **Actions** > **Restore snapshot**.

    ![Restore Snapshot](/images/5/00021.png?featherlight=false&width=90pc)

2.  **Cấu hình Instance Mới**:
    -   **DB instance identifier**: Nhập tên duy nhất cho instance mới (ví dụ: `workshop-db-restore`).
    -   **Instance specifications**: Chọn loại instance (ví dụ: `db.t3.micro`).
    -   **Connectivity**: Chọn cùng VPC và Subnet Group như instance gốc của bạn.
    -   **Security**: Chọn Security Group chính xác.

    **💡 Pro Tip**: Khi khôi phục để thử nghiệm, bạn có thể chọn loại instance nhỏ hơn để tiết kiệm chi phí.

    ![Restore Settings](/images/5/00022.png?featherlight=false&width=90pc)

3.  **Bắt đầu Khôi phục**:
    -   Nhấp vào **Restore DB instance**.

    **⚠️ Warning**: Quá trình khôi phục tạo ra một database instance hoàn toàn mới với endpoint mới. Bạn phải cập nhật chuỗi kết nối của ứng dụng để trỏ đến endpoint mới này.

    ![Restore Complete](/images/5/00027.png?featherlight=false&width=90pc)

4.  **Xác minh**:
    -   Đợi trạng thái chuyển sang **Available**.
    -   Kiểm tra kết nối đến instance mới.

    ![Verify Restore](/images/5/00028.png?featherlight=false&width=90pc)
