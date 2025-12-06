---
title: "Tạo IAM Roles"
date: "2025-10-27"
weight: 2
chapter: false
pre: " <b> 5.2.2 </b> "
---

# Tạo IAM Roles

Chúng ta cần tạo IAM Role cho Lambda function. Role này cấp quyền cho Lambda truy cập các dịch vụ AWS khác như S3 (cho tài sản), SES (cho email), và RDS (cho dữ liệu).

## 1. Tạo Lambda Execution Role

### CLI
```bash
# 1. Tạo file trust policy
echo '{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "lambda.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}' > lambda-trust-policy.json

# 2. Tạo role
aws iam create-role \
  --role-name lambda-execution-role \
  --assume-role-policy-document file://lambda-trust-policy.json

# 3. Gắn các policy chuẩn
aws iam attach-role-policy \
  --role-name lambda-execution-role \
  --policy-arn arn:aws:iam::aws:policy/service-role/AWSLambdaVPCAccessExecutionRole

aws iam attach-role-policy \
  --role-name lambda-execution-role \
  --policy-arn arn:aws:iam::aws:policy/CloudWatchLogsFullAccess
```

### AWS Console
1. Mở [IAM Console](https://console.aws.amazon.com/iam).
2. Vào **Roles** → **Create role**.
3. **Trusted entity type**: AWS service.
4. **Service**: Lambda.
5. Nhấn **Next**.
6. **Add permissions**: Tìm và chọn:
   - `AWSLambdaVPCAccessExecutionRole`
   - `CloudWatchLogsFullAccess`
7. Nhấn **Next**.
8. **Role name**: `lambda-execution-role`.
9. Nhấn **Create role**.

---

## 2. Thêm Quyền Tùy chỉnh (Custom Permissions)

Chúng ta cần cấp cho Lambda quyền truy cập cụ thể vào S3 bucket và RDS.

### CLI
```bash
# 1. Tạo file policy
echo '{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:PutObject",
        "s3:DeleteObject",
        "s3:ListBucket"
      ],
      "Resource": [
        "arn:aws:s3:::gametracker-assets/*",
        "arn:aws:s3:::gametracker-assets"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "ses:SendEmail",
        "ses:SendRawEmail"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "rds:DescribeDBInstances",
        "rds:DescribeDBProxies"
      ],
      "Resource": "*"
    }
  ]
}' > lambda-custom-policy.json

# 2. Gắn inline policy
aws iam put-role-policy \
  --role-name lambda-execution-role \
  --policy-name lambda-custom-permissions \
  --policy-document file://lambda-custom-policy.json
```

### AWS Console
1. Vào **Roles** và chọn `lambda-execution-role`.
2. Tại tab **Permissions**, nhấn **Add permissions** → **Create inline policy**.
3. Chọn trình soạn thảo **JSON** và dán nội dung JSON ở trên vào.
4. Nhấn **Next**.
5. **Policy name**: `lambda-custom-permissions`.
6. Nhấn **Create policy**.
