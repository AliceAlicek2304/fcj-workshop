---
title : "Triển khai ứng dụng"
date : "2025-10-27"
weight : 5
chapter : false
pre : " <b> 5.5 </b> "
---

#### Triển khai Ứng dụng Node.js

**ℹ️ Information**: Bây giờ hạ tầng của chúng ta (EC2 và RDS) đã sẵn sàng, chúng ta sẽ triển khai ứng dụng Node.js mẫu.

#### Bước 1: Clone Repository

1.  Kết nối vào EC2 instance của bạn qua SSH (nếu chưa kết nối).
2.  Clone repository của workshop:

    ```bash
    git clone https://github.com/AWS-First-Cloud-Journey/AWS-FCJ-Management
    cd AWS-FCJ-Management
    ```

#### Bước 2: Cài đặt các gói phụ thuộc

1.  Khởi tạo dự án và cài đặt các gói cần thiết:

    ```bash
    npm install
    ```

#### Bước 3: Cấu hình Kết nối Cơ sở dữ liệu

1.  Tạo một tệp `.env` để lưu trữ thông tin xác thực cơ sở dữ liệu của bạn:

    ```bash
    nano .env
    ```

2.  Dán nội dung sau vào, thay thế các giá trị giữ chỗ bằng thông tin RDS thực tế của bạn:

    ```env
    DB_HOST=your-rds-endpoint.us-east-1.rds.amazonaws.com
    DB_USER=admin
    DB_PASSWORD=your-password
    DB_NAME=workshopdb
    DB_PORT=3306
    ```

    -   **DB_HOST**: Endpoint bạn đã sao chép từ RDS console.
    -   **DB_USER**: Tên người dùng chính (Master username) bạn đã đặt (ví dụ: `admin`).
    -   **DB_PASSWORD**: Mật khẩu chính (Master password) bạn đã đặt.
    -   **DB_NAME**: Tên cơ sở dữ liệu (ví dụ: `workshopdb`).

3.  Lưu và thoát (`Ctrl+O`, `Enter`, `Ctrl+X`).

#### Bước 4: Khởi tạo Cơ sở dữ liệu

**ℹ️ Information**: Chúng ta cần tạo các bảng cần thiết cho ứng dụng. Chúng ta sẽ sử dụng một script đơn giản hoặc các lệnh SQL.

1.  Đảm bảo rằng ứng dụng của bạn có cơ chế để tạo bảng (migration) hoặc bạn có thể chạy một script khởi tạo. Nếu cần tạo bảng thủ công, bạn có thể sử dụng script Node.js sau:

    ```javascript
    const mysql = require('mysql');
    require('dotenv').config();

    const connection = mysql.createConnection({
      host: process.env.DB_HOST,
      user: process.env.DB_USER,
      password: process.env.DB_PASSWORD,
      database: process.env.DB_NAME
    });

    connection.connect();

    const createTableQuery = `
      CREATE TABLE IF NOT EXISTS users (
        id INT AUTO_INCREMENT PRIMARY KEY,
        name VARCHAR(255) NOT NULL,
        email VARCHAR(255) NOT NULL,
        created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
      )
    `;

    connection.query(createTableQuery, (error, results, fields) => {
      if (error) throw error;
      console.log('Table created successfully');
    });

    connection.end();
    ```

#### Bước 5: Khởi chạy Ứng dụng

1.  Khởi chạy ứng dụng bằng `npm`:

    ```bash
    npm start
    ```

    Bạn sẽ thấy thông báo cho biết máy chủ đang chạy (ví dụ: `Server running on port 3000` hoặc `5000`).

#### Bước 6: Xác minh Triển khai

1.  Mở trình duyệt web của bạn.
2.  Truy cập `http://<EC2-Public-IP>:5000` (hoặc cổng mà ứng dụng của bạn sử dụng).
3.  Bạn sẽ thấy ứng dụng của mình đang chạy và kết nối với cơ sở dữ liệu RDS.

    ![App Running](/images/5/00011.png?featherlight=false&width=90pc)

**💡 Pro Tip**: Nếu bạn không thể truy cập ứng dụng, hãy kiểm tra xem **EC2 Security Group** của bạn có cho phép lưu lượng truy cập đến (inbound) trên cổng ứng dụng (ví dụ: 5000) từ địa chỉ IP của bạn hay không.
