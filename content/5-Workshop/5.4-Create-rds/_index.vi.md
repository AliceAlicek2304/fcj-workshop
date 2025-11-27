---
title : "Tạo RDS database instance"
date : "2025-10-27"
weight : 4
chapter : false
pre : " <b> 5.4 </b> "
---

#### Chuẩn bị Môi trường EC2

**ℹ️ Information**: Trước khi tạo cơ sở dữ liệu, hãy chuẩn bị instance EC2 của chúng ta với các công cụ cần thiết (Git và Node.js) để chạy ứng dụng và kết nối với cơ sở dữ liệu.

1.  **Kết nối vào EC2 instance** qua SSH (như đã thực hiện ở bước trước).

2.  **Cài đặt Git**:
    Cập nhật hệ thống và cài đặt Git để sao chép mã nguồn ứng dụng.
    ```bash
    sudo dnf update -y
    sudo dnf install git -y
    git --version
    ```

3.  **Cài đặt Node.js**:
    Chúng ta sẽ sử dụng một script để cài đặt Node.js (phiên bản LTS) và các thư viện cần thiết.
    
    Tạo một file script:
    ```bash
    nano install_node.sh
    ```
    
    Dán nội dung sau vào:
    ```bash
    #!/bin/bash
    
    # Cài đặt nvm (Node Version Manager)
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash
    . ~/.nvm/nvm.sh
    
    # Cài đặt Node.js LTS
    nvm install --lts
    nvm use --lts
    
    # Kiểm tra cài đặt
    node -v
    npm -v
    
    # Cài đặt công cụ phát triển toàn cục
    npm install -g nodemon
    
    echo "Node.js installation complete."
    ```
    
    Lưu và thoát (`Ctrl+O`, `Enter`, `Ctrl+X`).
    
    Chạy script:
    ```bash
    bash install_node.sh
    ```

#### Tạo RDS Database Instance

**ℹ️ Information**: Bây giờ chúng ta sẽ tạo một instance cơ sở dữ liệu MySQL sử dụng Amazon RDS.

#### Hướng dẫn từng bước

1.  Điều hướng đến bảng điều khiển **Amazon RDS**.

2.  Nhấn **Create database**.

3.  **Choose a database creation method**: Chọn **Standard create**.

    ![Create RDS](/images/4/0004.png?featherlight=false&width=90pc)

4.  **Engine options**:
    - **Engine type**: Chọn **MySQL**.
    - **Edition**: Chọn **MySQL Community**.
    - **Version**: Chọn phiên bản mới nhất có sẵn (hoặc **MySQL 8.0.x**).

5.  **Templates**:
    - Chọn **Free tier** (nếu có và áp dụng) hoặc **Dev/Test** cho workshop này.
    
    **💡 Pro Tip**: Chọn **Free tier** sẽ tự động ẩn các tùy chọn phát sinh chi phí, chẳng hạn như Multi-AZ và Provisioned IOPS.

6.  **Settings**:
    - **DB instance identifier**: Nhập tên (ví dụ: `workshop-db`).
    - **Master username**: `admin` (hoặc tên người dùng bạn muốn).
    - **Master password**: Nhập mật khẩu mạnh và xác nhận lại.

    **⚠️ Warning**: Không sử dụng **Auto generate a password** trừ khi bạn lưu nó ngay lập tức. Tốt nhất là tự đặt mật khẩu cho workshop này để dễ nhớ.

    ![Create RDS](/images/4/0006.png?featherlight=false&width=90pc)

7.  **Instance configuration**:
    - **DB instance class**: Chọn **Burstable classes (includes t classes)** -> **db.t3.micro** (đủ điều kiện Free tier).

8.  **Storage**:
    - **Storage type**: General Purpose SSD (gp2 hoặc gp3).
    - **Allocated storage**: `20` GiB.

9.  **Connectivity**:
    - **Compute resource**: Chọn **Don't connect to an EC2 compute resource**.
    - **VPC**: Chọn VPC workshop của bạn.
    - **DB Subnet Group**: Chọn nhóm bạn đã tạo ở bước 5.2.4.
    - **Public access**: **No** (Thực hành tốt nhất về bảo mật).
    - **VPC security group**: Chọn **Choose existing** và chọn **RDS Security Group** đã tạo ở bước 5.2.3. Xóa security group `default` nếu có.

    **🔒 Security Note**: Đảm bảo Public access là **No** và sử dụng đúng Security Group để ngăn chặn truy cập trái phép từ internet vào cơ sở dữ liệu của bạn.

    ![Create RDS](/images/4/0009.png?featherlight=false&width=90pc)

10. **Additional configuration**:
    - **Initial database name**: Nhập `workshopdb` (Điều này cho phép RDS tự động tạo schema cho bạn).
    - Giữ nguyên các cài đặt khác.

11. Nhấn **Create database**.

    ![Create RDS](/images/4/00012.png?featherlight=false&width=90pc)

#### Xác minh Cơ sở dữ liệu

1.  Đợi cho đến khi **Status** chuyển từ `Creating` sang `Available`.
2.  Nhấp vào **DB identifier** (`workshop-db`) để xem chi tiết.
3.  Ghi lại **Endpoint** (ví dụ: `workshop-db.xxxxxx.us-east-1.rds.amazonaws.com`). Bạn sẽ cần thông tin này để kết nối ứng dụng của mình.

    ![Create RDS](/images/4/00017.png?featherlight=false&width=90pc)

#### Giám sát và Bảo trì

**ℹ️ Information**: RDS cung cấp các công cụ tích hợp để giám sát và bảo trì.

-   **Logs & Events**: Kiểm tra tab **Logs & events** để xem nhật ký lỗi, nhật ký truy vấn chậm và các sự kiện quản trị.
-   **Maintenance & backups**: Kiểm tra tab này để xem cửa sổ sao lưu và bất kỳ bản cập nhật bảo trì nào đang chờ xử lý.

**💡 Pro Tip**: Bật **Enhanced Monitoring** để có các chỉ số chi tiết, thời gian thực nếu bạn cần gỡ lỗi hiệu suất.
