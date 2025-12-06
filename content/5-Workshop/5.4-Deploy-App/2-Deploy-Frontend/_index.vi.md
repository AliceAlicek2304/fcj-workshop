---
title: "Deploy Frontend"
date: "2025-10-27"
weight: 2
chapter: false
pre: " <b> 5.4.2 </b> "
---

# Deploy Frontend (React + S3 + CloudFront)

## 1. Tạo S3 Buckets

Chúng ta cần hai bucket: một cho mã nguồn frontend và một cho tài sản game (assets).

### CLI
```bash
# Frontend Bucket
aws s3 mb s3://gametracker-frontend --region ap-southeast-2

# Assets Bucket
aws s3 mb s3://gametracker-assets --region ap-southeast-2
```

### AWS Console
1. **S3 Console** → **Create bucket**.
2. Tạo `gametracker-frontend` (tắt public access nếu dùng CloudFront OAC).
3. Tạo `gametracker-assets` (cấu hình CORS nếu cần).

---

## 2. Tạo CloudFront Distribution

Giúp phân phối nội dung nhanh chóng và hỗ trợ HTTPS.

### AWS Console
1. **CloudFront Console** → **Create distribution**.
2. **Origin domain**: Chọn `gametracker-frontend.s3...`.
3. **Origin access**: Chọn **Origin access control settings (recommended)** -> Tạo control setting.
   - *Quan trọng*: Bạn phải cập nhật S3 bucket policy để cho phép CloudFront truy cập (copy policy mà AWS cung cấp sau khi tạo).
4. **Viewer protocol policy**: Redirect HTTP to HTTPS.
5. **Default root object**: `index.html`.
6. **Error pages** (Trang lỗi):
   - Tạo custom error response cho **403** và **404** -> Path `/index.html` -> Status **200**.
   - Điều này rất quan trọng để SPA routing hoạt động.
7. Nhấn **Create**.

---

## 3. Build & Deploy React App

Cập nhật API URL trong ứng dụng React của bạn để trỏ tới API Gateway Invoke URL bạn đã lấy ở bước trước.

```bash
# 1. Build
npm run build

# 2. Sync lên S3
aws s3 sync build/ s3://gametracker-frontend

# 3. Xóa Cache (Tùy chọn nhưng khuyến nghị)
aws cloudfront create-invalidation --distribution-id <DISTRIBUTION_ID> --paths "/*"
```

Ứng dụng GameTracker của bạn hiện đã hoạt động tại tên miền CloudFront!
