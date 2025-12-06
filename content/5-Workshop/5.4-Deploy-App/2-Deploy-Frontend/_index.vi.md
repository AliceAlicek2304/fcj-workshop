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

## 3. Cấu hình và Build React App

Trước khi build, bạn phải trỏ Frontend tới API Gateway mới tạo.

1.  Mở thư mục `frontend` trong trình soạn thảo code.
2.  Tìm file cấu hình (thường là `.env` hoặc `src/config.js`).
3.  Cập nhật **API_URL** thành **API Gateway Invoke URL** của bạn (lấy từ bước 5.4.1).
    ```javascript
    // Ví dụ .env
    REACT_APP_API_URL=https://<api-id>.execute-api.ap-southeast-2.amazonaws.com
    ```
4.  Build ứng dụng:
    ```bash
    npm install
    npm run build
    ```

---

## 4. Upload lên S3

Đẩy các file đã build lên S3 bucket.

```bash
# Sync thư mục build lên S3
aws s3 sync build/ s3://gametracker-frontend

# Xóa Cache (để thấy thay đổi ngay lập tức)
aws cloudfront create-invalidation --distribution-id <DISTRIBUTION_ID> --paths "/*"
```

**🎉 Thành công!** Ứng dụng GameTracker của bạn hiện đã hoạt động tại tên miền CloudFront! Hãy truy cập trình duyệt để kiểm tra.
