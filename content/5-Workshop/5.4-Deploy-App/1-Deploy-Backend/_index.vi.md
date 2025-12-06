---
title: "Deploy Backend"
date: "2025-10-27"
weight: 1
chapter: false
pre: " <b> 5.4.1 </b> "
---

# Deploy Backend (Spring Boot + Lambda)

## 1. Tạo ECR Repository

### CLI
```bash
aws ecr create-repository \
  --repository-name gametracker-backend \
  --region ap-southeast-2 \
  --image-scanning-configuration scanOnPush=true
```

### AWS Console
1. Mở **ECR Console**.
2. Nhấn **Create repository**.
3. Name: `gametracker-backend`.
4. Nhấn **Create**.

---

## 2. Build & Push Docker Image

**Yêu cầu**: Máy local đã cài Docker và AWS CLI đã được cấu hình.

```bash
# 1. Login vào ECR
aws ecr get-login-password --region ap-southeast-2 | \
  docker login --username AWS --password-stdin <ACCOUNT_ID>.dkr.ecr.ap-southeast-2.amazonaws.com

# 2. Build ứng dụng Spring Boot (Maven/Gradle)
# cd backend
# ./mvnw clean package -DskipTests

# 3. Build Docker Image
docker build -t gametracker-backend .

# 4. Tag Image
docker tag gametracker-backend:latest <ACCOUNT_ID>.dkr.ecr.ap-southeast-2.amazonaws.com/gametracker-backend:latest

# 5. Push Image
docker push <ACCOUNT_ID>.dkr.ecr.ap-southeast-2.amazonaws.com/gametracker-backend:latest
```

---

## 3. Tạo Lambda Function

### CLI
```bash
aws lambda create-function \
  --function-name gametracker-api \
  --package-type Image \
  --code ImageUri=<ACCOUNT_ID>.dkr.ecr.ap-southeast-2.amazonaws.com/gametracker-backend:latest \
  --role arn:aws:iam::<ACCOUNT_ID>:role/lambda-execution-role \
  --memory-size 3008 \
  --timeout 60 \
  --region ap-southeast-2 \
  --vpc-config SubnetIds=<SUBNET_PRIVATE_1_ID>,<SUBNET_PRIVATE_2_ID>,SecurityGroupIds=<LAMBDA_SG_ID> \
  --environment Variables='{
    SPRING_PROFILES_ACTIVE=prod,
    SPRING_DATASOURCE_URL=jdbc:sqlserver://<RDS_ENDPOINT>:1433;databaseName=gametracker,
    SPRING_DATASOURCE_USERNAME=admin,
    SPRING_DATASOURCE_PASSWORD=your-password,
    AWS_S3_BUCKET=gametracker-assets,
    AWS_S3_REGION=ap-southeast-2
  }'
```

### AWS Console
1. Mở **Lambda Console** → **Create function**.
2. Chọn **Container image**.
3. Name: `gametracker-api`.
4. Image URI: Chọn từ ECR.
5. Role: Chọn role có sẵn `lambda-execution-role`.
6. **VPC Settings** (Advanced):
   - VPC: `gametracker-vpc`.
   - Subnets: Private subnets.
   - Security Group: `gametracker-lambda-sg`.
7. **Environment variables**: Thêm các biến `SPRING_DATASOURCE_URL`, v.v.
8. Nhấn **Create function**.

---

## 4. Tạo API Gateway (HTTP API)

### CLI
```bash
# Tạo API
aws apigatewayv2 create-api --name gametracker-api --protocol-type HTTP --target arn:aws:lambda:ap-southeast-2:<ACCOUNT_ID>:function:gametracker-api

# Cấp quyền
aws lambda add-permission --function-name gametracker-api --statement-id apigateway --action lambda:InvokeFunction --principal apigateway.amazonaws.com
```

### AWS Console
1. **API Gateway Console** → **Create API** → **HTTP API** (Build).
2. **Integrations**: Add integration -> Lambda -> `gametracker-api`.
3. **Name**: `gametracker-api`.
4. **Stages**: `$default` (Auto-deploy).
5. Nhấn **Create**.
6. Lưu lại **Invoke URL**.
