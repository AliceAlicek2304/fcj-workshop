---
title: "Bản đề xuất"
date: "2025-09-10"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# 1. TỔNG QUAN DỰ ÁN & MỤC TIÊU

## 1.1 TÓM TẮT DỰ ÁN (EXECUTIVE SUMMARY)
**Bối cảnh**
Thị trường game đang bùng nổ, kéo theo nhu cầu của người chơi trong việc theo dõi, phân tích dữ liệu và mô phỏng các cơ chế game. **GameTracker** ra đời như một giải pháp toàn diện giúp cả người chơi lẫn nhà quản trị (Admin) dễ dàng quản lý, chia sẻ và tra cứu thông tin về nhân vật, vũ khí và sự kiện.

**Vấn đề cần giải quyết**
-   **Dữ liệu phân mảnh**: Thông tin thường nằm rải rác trên nhiều wiki, bảng tính (spreadsheets), khó tra cứu tập trung.
-   **Rào cản ngôn ngữ**: Nhiều tựa game quốc tế chưa hỗ trợ tiếng Việt đầy đủ.
-   **Quản lý thủ công**: Admin tốn nhiều thời gian cập nhật dữ liệu thủ công, dễ sai sót.

**Giải pháp Đề xuất**
Xây dựng **GameTracker** - ứng dụng web hiện đại trên nền tảng điện toán đám mây **AWS**. Chúng tôi sử dụng kiến trúc **Serverless** để tối ưu chi phí vận hành, đồng thời đảm bảo khả năng chịu tải cao trong các đợt sự kiện game lớn.

## 1.2 MỤC TIÊU DỰ ÁN
-   **Số hóa & Tập trung hóa**: Một cổng thông tin duy nhất cho mọi dữ liệu game.
-   **Trải nghiệm người dùng vượt trội**: Cung cấp các công cụ giá trị như Giả lập Gacha (Gacha Simulator), Lịch trình sự kiện (Event Timeline).
-   **Vận hành thông minh**: Hệ thống tự động mở rộng theo lưu lượng truy cập, "dùng bao nhiêu trả bấy nhiêu".

---

# 2. KIẾN TRÚC GIẢI PHÁP

## 2.1 MÔ HÌNH KIẾN TRÚC (HIGH-LEVEL ARCHITECTURE)
Hệ thống được thiết kế dựa trên các nguyên lý của **AWS Well-Architected Framework**, ưu tiên tính Tin cậy (Reliability) và Tối ưu Chi phí (Cost Optimization).

**Sơ đồ Kiến trúc**:

![Architecture](/images/2-Proposal/GameTracker1.jpg)

**Các thành phần cốt lõi**:
1.  **Frontend (Lớp Hiển thị)**:
    -   Xây dựng bằng **ReactJS (Vite)** cho trải nghiệm mượt mà, tốc độ cao.
    -   Lưu trữ static content trên **Amazon S3** và phân phối toàn cầu qua CDN **Amazon CloudFront**.
    -   Bảo vệ bởi tường lửa ứng dụng web **AWS WAF**.

2.  **Backend (Lớp Xử lý)**:
    -   Viết bằng **Spring Boot (Java)**, đóng gói trong **Docker Container**.
    -   Chạy trên nền tảng **AWS Lambda** (Serverless Compute) để loại bỏ gánh nặng quản lý máy chủ.
    -   Giao tiếp qua **API Gateway (HTTP API)** đảm bảo bảo mật và hiệu năng.

3.  **Database (Lớp dữ liệu)**:
    -   **Amazon RDS (SQL Server Express)**: Lưu trữ các dữ liệu có cấu trúc phức tạp (Hồ sơ người dùng, Chỉ số nhân vật).
    -   **Amazon S3**: Lưu trữ tài nguyên đa phương tiện (Ảnh nhân vật, Icon vũ khí) với độ bền dữ liệu cực cao.

4.  **Bảo mật & Định danh**:
    -   **Google OAuth2**: Đăng nhập nhanh chóng, không cần nhớ mật khẩu.
    -   **AWS IAM**: Quản lý quyền truy cập chặt chẽ cho từng tài nguyên (Least Privilege).
    -   **Security Groups**: Tường lửa ảo kiểm soát lưu lượng ra/vào hạ tầng.

## 2.2 CÔNG NGHỆ SỬ DỤNG
-   **Ngôn ngữ**: Java 17, TypeScript/JavaScript.
-   **Frameworks**: Spring Boot 3, React 18.
-   **DevOps**: Docker, AWS CLI, GitHub Actions.
-   **Cơ sở dữ liệu**: Microsoft SQL Server 2022.

---

# 3. KẾ HOẠCH TRIỂN KHAI

## 3.1 CÁC GIAI ĐOẠN (MILESTONES)
Dự án được thực hiện theo mô hình Agile trong 4 tuần:

| Giai đoạn | Thời gian | Hoạt động chính | Sản phẩm bàn giao |
|-----------|-----------|-----------------|-------------------|
| **P1. Phân tích & Thiết kế** | Tuần 1 | Thu thập yêu cầu, Thiết kế CSDL, Dựng VPC trên AWS | Tài liệu kiến trúc, Môi trường AWS |
| **P2. Phát triển Backend** | Tuần 2 | Viết API, Tích hợp đăng nhập (Auth), Kết nối DB | RESTful API hoàn chỉnh, Swagger Docs |
| **P3. Phát triển Frontend** | Tuần 3 | Ghép giao diện, Xử lý logic Gacha, Dashboard Admin | Ứng dụng Web hoàn chỉnh |
| **P4. Vận hành & Chuyển giao** | Tuần 4 | Thiết lập CI/CD, Kiểm thử, Viết tài liệu | Hướng dẫn sử dụng, Web đã online |

## 3.2 LỘ TRÌNH LÊN PRODUCTION
-   **Môi trường**: Phân tách rõ ràng giữa Development và Production.
-   **Khả năng mở rộng**: Thiết kế Serverless cho phép đáp ứng từ 0 đến 10.000 người dùng đồng thời mà không cần can thiệp thủ công.
-   **Giám sát**: Tích hợp **Amazon CloudWatch** để theo dõi log và cảnh báo lỗi theo thời gian thực.

---

# 4. ƯỚC TÍNH CHI PHÍ
**Chi phí AWS dự kiến hàng tháng**: ~$123.00 (Khoảng 3.000.000 VNĐ)

| Dịch vụ | Mức sử dụng ước tính | Chi phí (xấp xỉ) |
|---------|----------------------|------------------|
| **RDS (SQL Server)** | db.t3.micro (Single AZ) | ~$60.00 |
| **NAT Gateway** | 1 Unit (nếu cần thiết) | ~$32.00 |
| **AWS WAF** | Web ACL + Phí request | ~$10.00 |
| **CloudFront** | 100GB Lưu lượng ra | ~$8.50 |
| **AWS Lambda** | 1 Triệu lần gọi (Invocations) | ~$5.00 |
| **Khác (S3, logs)** | Gói tiêu chuẩn | ~$7.50 |

*Lưu ý: Có thể tối ưu chi phí bằng cách tắt NAT Gateway và RDS khi không sử dụng (môi trường Dev).*

---

# 5. ĐỘI NGŨ THỰC HIỆN

Dự án được thực hiện bởi nhân sự Full Stack chuyên trách, đảm bảo tính nhất quán từ thiết kế đến vận hành.

| Họ và Tên | Vai trò | Email liên hệ | Trách nhiệm chính |
|-----------|---------|---------------|-------------------|
| **Nguyễn Văn Cường** | Full Stack Developer | `cuongnvse183645@fpt.edu.vn` | Kiến trúc hệ thống, Lập trình Frontend/Backend, DevOps, Triển khai AWS |

---

# 6. TIÊU CHÍ NGHIỆM THU (ACCEPTANCE)

Sản phẩm được coi là hoàn thành khi đáp ứng các luồng nghiệp vụ sau:
1.  **Đăng nhập**: Người dùng đăng nhập thành công qua Google.
2.  **Quản lý dữ liệu**: Admin có thể Thêm/Sửa/Xóa nhân vật game thông qua Dashboard.
3.  **Giả lập**: Tính năng Gacha trả về kết quả ngẫu nhiên dựa trên tỉ lệ được cài đặt.
4.  **Triển khai**: Ứng dụng truy cập được từ internet thông qua domain CloudFront với HTTPS.

<br>

<h3 style="font-size: 1.3em;">🔗 Trải nghiệm ngay: <a href="https://d2eu9it59oopt8.cloudfront.net/" target="_blank">https://d2eu9it59oopt8.cloudfront.net/</a></h3>