---
title: "Bản đề xuất"
date: "2025-09-10"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# GameTracker Platform for Game Community
## Giải pháp AWS Serverless hợp nhất cho quản lý và chia sẻ dữ liệu game

### 1. Tóm tắt
GameTracker là nền tảng dành cho **người chơi và admin** để quản lý, theo dõi và chia sẻ thông tin về nhân vật, vũ khí, banner, vật phẩm và sự kiện trong game. Hệ thống hỗ trợ đăng nhập đa phương thức (email/password, Google OAuth2), quản lý tài khoản, dashboard admin, và lưu trữ file trên **AWS S3**.  

Frontend là **React SPA**, phục vụ qua **S3 + CloudFront**, được bảo vệ bởi **AWS WAF** để đảm bảo bảo mật và hiệu năng. Backend sử dụng **Spring Boot serverless** trên **AWS Lambda**, kết nối với **SQL Server (RDS)**.  

GameTracker cung cấp **công cụ trực quan**:  
- **Tracker lịch sử gacha** của tài khoản, dễ theo dõi  
- **Giả lập gacha** giúp dự đoán kết quả rút  
- **Timeline banner/event** hiển thị thông tin và thời gian diễn ra sự kiện  

Giúp người chơi quản lý dữ liệu hiệu quả, đặc biệt với **game tiếng Anh** khó tiếp cận.  

---

### 2. Vấn đề
**Vấn đề hiện tại**  
Người chơi gặp khó khăn khi quản lý và tra cứu dữ liệu game, đặc biệt với các game gacha phức tạp. Game tiếng Anh khiến thông tin khó tiếp cận với một số người dùng.  

**Giải pháp**  
GameTracker cung cấp **hệ thống tập trung, dễ dùng** cho người dùng:  
- Quản lý và cập nhật dữ liệu game  
- Theo dõi lịch sử gacha, giả lập gacha  
- Xem timeline banner và event  

Admin có thể kiểm soát nội dung với **CRUD và phân quyền rõ ràng**.  

**Lợi ích và Lợi tức đầu tư (ROI)**
- Tối ưu quản lý dữ liệu cho người dùng và admin  
- Giảm thời gian bảo trì thủ công, nâng cao độ tin cậy dữ liệu  
- Chi phí vận hành thấp nhờ AWS serverless & S3  
- Dễ mở rộng cho nhiều game và tính năng cộng đồng  

---

### 3. Kiến trúc giải pháp
**Kiến trúc cloud hiện đại:**  

- **Frontend:** React SPA, S3 + CloudFront, SPA fallback, bảo vệ bằng **AWS WAF**  
- **Backend:** Spring Boot serverless trên Lambda, JWT, Google OAuth2, API bảo vệ bởi WAF  
- **Database:** SQL Server (**RDS**)  
- **File Storage:** AWS S3 (avatar, background, vũ khí, banner)  
- **Admin Dashboard:** CRUD, phân quyền  
- **Bảo mật:** Spring Security, CORS, AWS WAF  

![IoT Weather Station Architecture](/images/2-Proposal/GameTracker.jpg)

**Dịch vụ AWS sử dụng**  
- AWS S3: lưu trữ file tĩnh và media  
- AWS Lambda: backend serverless  
- AWS RDS: lưu trữ dữ liệu game  
- AWS CloudFront: phân phối SPA  
- AWS WAF: bảo vệ frontend & API  
- AWS SES: email xác thực, reset mật khẩu  
- AWS IAM: quản lý quyền truy cập  

**Thiết kế thành phần**  
- **User:** đăng ký, đăng nhập, quản lý tài khoản, avatar  
- **Admin:** quản lý dữ liệu game, CRUD, phân quyền  
- **Game Data:** nhân vật, vũ khí, banner, echo, setecho, role, element, background  
- **Tools:** tracker gacha, giả lập gacha, timeline banner/event  

---

### 4. Triển khai kỹ thuật
**Các giai đoạn triển khai**  
1. Phân tích yêu cầu, thiết kế kiến trúc  
2. Xây dựng backend Spring Boot serverless, JWT, Google OAuth2, kết nối RDS  
3. Xây dựng frontend React SPA, dashboard admin, các công cụ gacha và timeline  
4. Triển khai AWS: S3, CloudFront, SPA fallback, WAF  
5. Kiểm thử, tối ưu bảo mật, hoàn thiện tài liệu  

**Yêu cầu kỹ thuật**  
- Frontend: React, TypeScript, Vite, SPA fallback  
- Backend: Spring Boot, Spring Security, JWT, Google OAuth2, Lambda serverless  
- Database: SQL Server (RDS)  
- Cloud: S3, CloudFront, Lambda, WAF, SES  
- DevOps: Docker, CI/CD, AWS IAM  

---

### 5. Lộ trình & Mốc triển khai (1 tháng)
| Tuần | Giai đoạn | Nhiệm vụ |
|------|-----------|----------|
| Tuần 1 | Lập kế hoạch & Chuẩn bị | Phân tích yêu cầu, thiết kế kiến trúc, chuẩn bị AWS (S3, RDS, Lambda, WAF, CloudFront) |
| Tuần 2 | Phát triển Backend | Xây dựng backend, JWT, Google OAuth2, API endpoints, kết nối RDS, triển khai Lambda & WAF |
| Tuần 3 | Phát triển Frontend | Xây dựng React SPA, dashboard admin, các công cụ gacha, timeline banner/event |
| Tuần 4 | Triển khai & Kiểm thử | Triển khai SPA S3 + CloudFront, SPA fallback, WAF, kiểm thử, tối ưu bảo mật, hoàn thiện tài liệu |

---

### 6. Ước tính ngân sách

- AWS Lambda — Memory: 3008 MB, ~12,000 invocations/tháng (8,640 warmer + user traffic) ~ $5-7/tháng
- S3 Standard — 10 GB lưu trữ ~ $0.23/tháng
- CloudFront — 100 GB egress ~ $8.50/tháng
- RDS (SQL Server, production) ~ $60+/tháng
- SES — Giá tham khảo: ~ $0.01/tháng
- CloudWatch — Logs/metrics (10 GB logs) ~ $5/tháng
- AWS WAF — Web ACL + 1M requests ~ $10/tháng
- Route53 — 1 hosted zone + 1M queries ~ $0.90/tháng
- NAT Gateway — ~$32/tháng (data processing $0.045/GB)
- Tổng ≈ $121-123/tháng

---

### 7. Đánh giá rủi ro 
- AWS downtime: Ảnh hưởng trung bình, xác suất thấp  
- Tấn công bảo mật: Ảnh hưởng cao, xác suất thấp  
- Chi phí tăng cao: Ảnh hưởng trung bình, xác suất trung bình
- Lỗi dữ liệu do admin nhập sai: Ảnh hưởng trung bình, xác suất thấp  

**Chiến lược giảm thiểu**  
- Dùng AWS WAF, IAM hạn chế quyền, HTTPS, JWT an toàn  
- Theo dõi chi phí bằng CloudWatch, tối ưu truy vấn và cachiní  
- Dùng RDS Multi-AZ, CloudFront CDN, rollback nhanh khi lỗi  

**Kế hoạch dự phòng**  
- RDS failover khi sự cố 
- Rollback backend bằng Lambda Versioning


---

### 8. Kết quả kỳ vọng
- Hệ thống ổn định, tự mở rộng, chi phí thấp
- API bảo mật, dữ liệu tập trung và dễ quản lý
- Dễ mở rộng thêm game và tính năng
- Công cụ gacha và timeline giúp người chơi theo dõi thuận tiện

---

### 9. Tính năng trong tương lai

- 📊 Quản lý tài nguyên thời gian thực - Theo dõi materials, mora, exp books
- 🔍 Tra cứu thông tin theo UID - Tìm kiếm player profile và stats
- 🐧 Hỗ trợ Linux - PowerShell script cho Linux shell (bash/zsh)
- 📱 Mobile App - Ứng dụng di động iOS/Android
- 🔔 Thông báo banner mới - Push notification khi có banner mới
- 📈 Thống kê nâng cao - Deeper analytics cho gacha history

---

<h3 style="font-size: 1.3em;">🔗 Website dự án: <a href="https://d2eu9it59oopt8.cloudfront.net/" target="_blank">https://d2eu9it59oopt8.cloudfront.net/</a></h3>