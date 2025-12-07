---
title: "Bản đề xuất"
date: "2025-09-10"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# 1. BỐI CẢNH VÀ ĐỘNG LỰC (BACKGROUND AND MOTIVATION)

## 1.1 TÓM TẮT ĐIỀU HÀNH (EXECUTIVE SUMMARY)
**Bối cảnh**
Thị trường game đang phát triển mạnh cùng nhu cầu quản lý thông tin của người chơi. **GameTracker** là ứng dụng web cloud-native giúp người chơi và admin quản lý thông tin nhân vật, vũ khí, sự kiện một cách tập trung, giải quyết vấn đề dữ liệu bị phân mảnh trên nhiều nền tảng.

**Phạm vi chức năng (MVP)**
1.  **Thông tin Game**: Tra cứu chỉ số Nhân vật, Vũ khí, Vật phẩm.
2.  **Giả lập Gacha**: Mô phỏng quay thưởng thử nghiệm tỷ lệ rơi (drop-rate).
3.  **Lịch sử Gacha**: Công cụ import và phân tích lịch sử quay, đếm pity.
4.  **Timeline Sự kiện**: Lịch trình trực quan các sự kiện trong game.

**Đang phát triển**
1.  **Check Tài nguyên Real-time**: Đồng bộ nhựa/nguyên thạch thời gian thực.
2.  **Hệ thống thông báo**: Cảnh báo tài nguyên đầy.

## 1.2 TIÊU CHÍ THÀNH CÔNG (PROJECT SUCCESS CRITERIA)
-   **Hiệu suất**: Độ trễ API < 200ms cho 95% request.
-   **Độ sẵn sàng**: Uptime 99.9% trong tháng đầu tiên.
-   **Chi phí**: Chi phí hạ tầng AWS dưới $150/tháng.

## 1.3 GIẢ ĐỊNH (ASSUMPTIONS)
-   **Quyền truy cập**: Team phát triển có quyền Admin vào AWS Account.
-   **Dịch vụ bên thứ 3**: Các dịch vụ Google OAuth2 và API của Game hoạt động ổn định.
-   **Dữ liệu**: Các asset hình ảnh/thông số game được phép sử dụng cho mục đích học tập/demo.
-   **Ngân sách**: Dự án tận dụng tối đa AWS Free Tier, chỉ trả phí cho các dịch vụ bắt buộc như NAT Gateway/RDS.

# 2. KIẾN TRÚC GIẢI PHÁP (SOLUTION ARCHITECTURE)

## 2.1 SƠ ĐỒ KIẾN TRÚC KỸ THUẬT
Hệ thống sử dụng kiến trúc Serverless trên AWS để tối ưu chi phí và khả năng mở rộng.

![Architecture](/images/2-Proposal/GameTracker1.jpg)

**Thành phần**:
-   Frontend: ReactJS (Vite) trên S3 + CloudFront.
-   Backend: Spring Boot trên Lambda + API Gateway.
-   Database: SQL Server trên RDS.
-   Bảo mật: WAF, IAM, Security Groups.

## 2.2 KẾ HOẠCH KỸ THUẬT (TECHNICAL PLAN)
-   **Frontend**: Phát triển bằng React/TypeScript, deploy tự động lên S3.
-   **Backend**: Spring Boot 3 đóng gói Docker, push lên ECR và chạy bằng Lambda.
-   **Hạ tầng**: Quản lý bằng AWS Console và CLI script.
-   **Testing**: Unit test cho logic backend và kiểm thử thủ công cho luồng UI.

## 2.3 KẾ HOẠCH DỰ ÁN (PROJECT PLAN)
Dự án thực hiện trong 4 tuần (Agile):
-   **Tuần 1**: Phân tích, thiết kế DB, dựng VPC.
-   **Tuần 2**: Code API Backend & Kết nối DB.
-   **Tuần 3**: Code giao diện Frontend & Logic Gacha.
-   **Tuần 4**: Tích hợp, CI/CD, Deploy và viết tài liệu.

## 2.4 CÂN NHẮC VỀ BẢO MẬT (SECURITY CONSIDERATIONS)
-   **Định danh**: Sử dụng Google OAuth2 và JWT.
-   **Mạng**: VPC chia Public/Private subnet; Database nằm trong Private subnet.
-   **Mã hóa**: HTTPS cho đường truyền; RDS encrypted at-rest.
-   **Phân quyền**: IAM Roles theo nguyên tắc quyền tối thiểu (Least Privilege).

# 3. HOẠT ĐỘNG VÀ BÀN GIAO (ACTIVITIES AND DELIVERABLES)

## 3.1 CÁC HOẠT ĐỘNG VÀ SẢN PHẨM
| Giai đoạn | Hoạt động | Sản phẩm bàn giao |
|-----------|-----------|-------------------|
| **Thiết lập** | Tạo VPC, IAM, Git repo | Môi trường AWS, Tài liệu kiến trúc |
| **Phát triển** | Code API, UI, Migration | Source Code, Docker Images |
| **Triển khai** | Sync S3, Deploy Lambda, Config CloudFront | Website hoạt động, API Endpoint |

## 3.2 NGOÀI PHẠM VI (OUT OF SCOPE)
-   Ứng dụng Mobile (iOS/Android Native).
-   Tính năng Multiplayer thời gian thực (Lobby game).
-   Tích hợp cổng thanh toán tiền thật.

## 3.3 ĐƯỜNG ĐẾN PRODUCTION (PATH TO PRODUCTION)
-   **Mở rộng**: Lambda auto-scaling chịu tải 10,000 users.
-   **Giám sát**: CloudWatch Dashboard theo dõi lỗi và độ trễ.
-   **Backup**: RDS Automated Backup và S3 Versioning.

# 4. ƯỚC TÍNH CHI PHÍ AWS (AWS COST BREAKDOWN)
**Ước tính**: ~$123.00/tháng

| Dịch vụ | Ước tính | Chi phí |
|---------|----------|---------|
| **RDS (SQL Server)** | db.t3.micro | ~$60.00 |
| **NAT Gateway** | 1 Unit | ~$32.00 |
| **AWS WAF** | Web ACL | ~$10.00 |
| **CloudFront** | 100GB Data Out | ~$8.50 |
| **AWS Lambda** | 1M Invocations | ~$5.00 |
| **Khác** | S3, Logs | ~$7.50 |

# 5. ĐỘI NGŨ (TEAM)

| Tên | Vai trò | Email | Trách nhiệm |
|-----|---------|-------|-------------|
| **Nguyễn Văn Cường** | Full Stack Developer | `cuongnvse183645@fpt.edu.vn` | Thực hiện toàn trình (End-to-end) |

# 6. TÀI NGUYÊN & ƯỚC TÍNH NỖ LỰC (RESOURCES & ESTIMATES)
*Chi phí nhân sự tham khảo (Ngữ cảnh Workshop/Đồ án)*

| Tài nguyên | Trách nhiệm | Ước tính nỗ lực |
|------------|-------------|-----------------|
| Full Stack Developer | Thiết kế, Code, Deploy | ~160 Giờ (4 Tuần) |
| Technical Mentor | Review, Hướng dẫn | ~20 Giờ |

**Tổng nỗ lực dự kiến**: 4 Tuần/người (Man-weeks).

# 7. NGHIỆM THU (ACCEPTANCE)

Sản phẩm được nghiệm thu khi hoàn thành:
1.  **Login**: Đăng nhập Google thành công.
2.  **Quản lý**: Admin thêm/sửa/xóa được dữ liệu.
---
title: "Bản đề xuất"
date: "2025-09-10"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# 1. BỐI CẢNH VÀ ĐỘNG LỰC (BACKGROUND AND MOTIVATION)

## 1.1 TÓM TẮT ĐIỀU HÀNH (EXECUTIVE SUMMARY)
**Bối cảnh**
Thị trường game đang phát triển mạnh cùng nhu cầu quản lý thông tin của người chơi. **GameTracker** là ứng dụng web cloud-native giúp người chơi và admin quản lý thông tin nhân vật, vũ khí, sự kiện một cách tập trung, giải quyết vấn đề dữ liệu bị phân mảnh trên nhiều nền tảng.

**Phạm vi chức năng (MVP)**
1.  **Thông tin Game**: Tra cứu chỉ số Nhân vật, Vũ khí, Vật phẩm.
2.  **Giả lập Gacha**: Mô phỏng quay thưởng thử nghiệm tỷ lệ rơi (drop-rate).
3.  **Lịch sử Gacha**: Công cụ import và phân tích lịch sử quay, đếm pity.
4.  **Timeline Sự kiện**: Lịch trình trực quan các sự kiện trong game.

**Đang phát triển**
1.  **Check Tài nguyên Real-time**: Đồng bộ nhựa/nguyên thạch thời gian thực.
2.  **Hệ thống thông báo**: Cảnh báo tài nguyên đầy.

## 1.2 TIÊU CHÍ THÀNH CÔNG (PROJECT SUCCESS CRITERIA)
-   **Hiệu suất**: Độ trễ API < 200ms cho 95% request.
-   **Độ sẵn sàng**: Uptime 99.9% trong tháng đầu tiên.
-   **Chi phí**: Chi phí hạ tầng AWS dưới $150/tháng.

## 1.3 GIẢ ĐỊNH (ASSUMPTIONS)
-   **Quyền truy cập**: Team phát triển có quyền Admin vào AWS Account.
-   **Dịch vụ bên thứ 3**: Các dịch vụ Google OAuth2 và API của Game hoạt động ổn định.
-   **Dữ liệu**: Các asset hình ảnh/thông số game được phép sử dụng cho mục đích học tập/demo.
-   **Ngân sách**: Dự án tận dụng tối đa AWS Free Tier, chỉ trả phí cho các dịch vụ bắt buộc như NAT Gateway/RDS.

# 2. KIẾN TRÚC GIẢI PHÁP (SOLUTION ARCHITECTURE)

## 2.1 SƠ ĐỒ KIẾN TRÚC KỸ THUẬT
Hệ thống sử dụng kiến trúc Serverless trên AWS để tối ưu chi phí và khả năng mở rộng.

![Architecture](/images/2-Proposal/GameTracker1.jpg)

**Thành phần**:
-   Frontend: ReactJS (Vite) trên S3 + CloudFront.
-   Backend: Spring Boot trên Lambda + API Gateway.
-   Database: SQL Server trên RDS.
-   Bảo mật: WAF, IAM, Security Groups.

## 2.2 KẾ HOẠCH KỸ THUẬT (TECHNICAL PLAN)
-   **Frontend**: Phát triển bằng React/TypeScript, deploy tự động lên S3.
-   **Backend**: Spring Boot 3 đóng gói Docker, push lên ECR và chạy bằng Lambda.
-   **Hạ tầng**: Quản lý bằng AWS Console và CLI script.
-   **Testing**: Unit test cho logic backend và kiểm thử thủ công cho luồng UI.

## 2.3 KẾ HOẠCH DỰ ÁN (PROJECT PLAN)
Dự án thực hiện trong 4 tuần (Agile):
-   **Tuần 1**: Phân tích, thiết kế DB, dựng VPC.
-   **Tuần 2**: Code API Backend & Kết nối DB.
-   **Tuần 3**: Code giao diện Frontend & Logic Gacha.
-   **Tuần 4**: Tích hợp, CI/CD, Deploy và viết tài liệu.

## 2.4 CÂN NHẮC VỀ BẢO MẬT (SECURITY CONSIDERATIONS)
-   **Định danh**: Sử dụng Google OAuth2 và JWT.
-   **Mạng**: VPC chia Public/Private subnet; Database nằm trong Private subnet.
-   **Mã hóa**: HTTPS cho đường truyền; RDS encrypted at-rest.
-   **Phân quyền**: IAM Roles theo nguyên tắc quyền tối thiểu (Least Privilege).

# 3. HOẠT ĐỘNG VÀ BÀN GIAO (ACTIVITIES AND DELIVERABLES)

## 3.1 CÁC HOẠT ĐỘNG VÀ SẢN PHẨM
| Giai đoạn | Hoạt động | Sản phẩm bàn giao |
|-----------|-----------|-------------------|
| **Thiết lập** | Tạo VPC, IAM, Git repo | Môi trường AWS, Tài liệu kiến trúc |
| **Phát triển** | Code API, UI, Migration | Source Code, Docker Images |
| **Triển khai** | Sync S3, Deploy Lambda, Config CloudFront | Website hoạt động, API Endpoint |

## 3.2 NGOÀI PHẠM VI (OUT OF SCOPE)
-   Ứng dụng Mobile (iOS/Android Native).
-   Tính năng Multiplayer thời gian thực (Lobby game).
-   Tích hợp cổng thanh toán tiền thật.

## 3.3 ĐƯỜNG ĐẾN PRODUCTION (PATH TO PRODUCTION)
-   **Mở rộng**: Lambda auto-scaling chịu tải 10,000 users.
-   **Giám sát**: CloudWatch Dashboard theo dõi lỗi và độ trễ.
-   **Backup**: RDS Automated Backup và S3 Versioning.

# 4. ƯỚC TÍNH CHI PHÍ AWS (AWS COST BREAKDOWN)
**Ước tính**: ~$123.00/tháng

| Dịch vụ | Ước tính | Chi phí |
|---------|----------|---------|
| **RDS (SQL Server)** | db.t3.micro | ~$60.00 |
| **NAT Gateway** | 1 Unit | ~$32.00 |
| **AWS WAF** | Web ACL | ~$10.00 |
| **CloudFront** | 100GB Data Out | ~$8.50 |
| **AWS Lambda** | 1M Invocations | ~$5.00 |
| **Khác** | S3, Logs | ~$7.50 |

# 5. ĐỘI NGŨ (TEAM)

| Tên | Vai trò | Email | Trách nhiệm |
|-----|---------|-------|-------------|
| **Nguyễn Văn Cường** | Full Stack Developer | `cuongnvse183645@fpt.edu.vn` | Thực hiện toàn trình (End-to-end) |

# 6. TÀI NGUYÊN & ƯỚC TÍNH NỖ LỰC (RESOURCES & ESTIMATES)
*Chi phí nhân sự tham khảo (Ngữ cảnh Workshop/Đồ án)*

| Tài nguyên | Trách nhiệm | Ước tính nỗ lực |
|------------|-------------|-----------------|
| Full Stack Developer | Thiết kế, Code, Deploy | ~160 Giờ (4 Tuần) |
| Technical Mentor | Review, Hướng dẫn | ~20 Giờ |

**Tổng nỗ lực dự kiến**: 4 Tuần/người (Man-weeks).

# 7. NGHIỆM THU (ACCEPTANCE)

Sản phẩm được nghiệm thu khi hoàn thành:
1.  **Login**: Đăng nhập Google thành công.
2.  **Quản lý**: Admin thêm/sửa/xóa được dữ liệu.
3.  **Giả lập**: Gacha chạy đúng logic tỉ lệ.
4.  **Triển khai**: Web truy cập được qua HTTPS công khai.
5.  **Tài liệu**: Có hướng dẫn sử dụng và triển khai đầy đủ.

<br>

<h3 style="font-size: 1.3em;">🔗 Project Website: <a href="https://d2eu9it59oopt8.cloudfront.net/" target="_blank">https://d2eu9it59oopt8.cloudfront.net/</a></h3>
<h3 style="font-size: 1.3em;">📥 Tải về bản đề xuất: <a href="/files/Proposal-TeamOne.docx" download>Proposal-TeamOne.docx</a></h3>