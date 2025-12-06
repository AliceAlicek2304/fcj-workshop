---
title: "Backup & Restore"
date: "2025-10-27"
weight: 6
chapter: false
pre: " <b> 5.6 </b> "
---

# Chiến lược Sao lưu và Phục hồi

Đối với ứng dụng GameTracker, dữ liệu là tài sản quan trọng nhất. Chúng ta cần bảo vệ:
1.  **Dữ liệu Game có cấu trúc**: Lưu trong **Amazon RDS (SQL Server)**.
2.  **Tài sản Game (Assets)**: Hình ảnh và file lưu trong **Amazon S3**.

## 1. Sao lưu RDS (SQL Server)

Amazon RDS cung cấp hai phương pháp khác nhau để sao lưu DB instance của bạn:

### A. Sao lưu Tự động (Automated Backups)
Khi tạo RDS instance, chúng ta đã bật tính năng **Automated backups**.
-   **Thời gian lưu trữ**: Chúng ta đã thiết lập là **7 ngày**.
-   **Chức năng**: AWS tạo snapshot cho storage volume của DB instance, sao lưu toàn bộ instance lên S3.
-   **Phục hồi theo thời điểm (Point-in-Time Recovery)**: Bạn có thể khôi phục cơ sở dữ liệu về bất kỳ giây nào trong thời gian lưu trữ.

### B. Snapshot Thủ công (Manual Snapshots)
Bạn có thể tạo snapshot cho database bất kỳ lúc nào. Khác với sao lưu tự động, snapshot thủ công được lưu trữ mãi mãi cho đến khi bạn tự tay xóa chúng.

**Các bước tạo Snapshot Thủ công:**
1.  Mở [RDS Console](https://console.aws.amazon.com/rds).
2.  Vào **Databases** -> Chọn `gametracker-mssql`.
3.  Nhấn **Actions** -> **Take snapshot**.
4.  Thông tin:
    -   **Snapshot name**: `gametracker-manual-backup-v1`.
5.  Nhấn **Take snapshot**.

![RDS Snapshot](/images/5/00019.png?featherlight=false&width=90pc)

---

## 2. Bảo vệ Dữ liệu S3

Đối với bucket `gametracker-assets`, chúng ta nên bật tính năng **Versioning** (Phiên bản). Tính năng này cho phép lưu giữ, truy xuất và khôi phục mọi phiên bản của mọi đối tượng được lưu trong bucket.

**Các bước bật Versioning:**
1.  Mở [S3 Console](https://console.aws.amazon.com/s3).
2.  Chọn bucket **gametracker-assets**.
3.  Chuyển sang tab **Properties**.
4.  Tại mục **Bucket Versioning**, nhấn **Edit**.
5.  Chọn **Enable**.
6.  Nhấn **Save changes**.

Giờ đây, nếu admin lỡ tay xóa hoặc ghi đè nhầm hình ảnh nhân vật, bạn có thể dễ dàng khôi phục lại phiên bản trước đó.

---

## 3. Chiến lược Khôi phục (Restore)

Trong trường hợp có sự cố (ví dụ: xóa nhầm dữ liệu trong SQL Server):
1.  Vào **RDS Console** -> **Snapshots**.
2.  Chọn snapshot mới nhất (Tự động hoặc Thủ công).
3.  Nhấn **Actions** -> **Restore snapshot**.
4.  **New DB Instance Identifier**: ví dụ `gametracker-mssql-restore`.
5.  Sau khi instance mới đã sẵn sàng (Available), hãy cập nhật **Lambda Environment Variables** (`SPRING_DATASOURCE_URL`) để trỏ tới endpoint mới.
