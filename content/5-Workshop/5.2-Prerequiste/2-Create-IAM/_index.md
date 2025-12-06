---
title: "Create IAM Roles"
date: "2025-10-27"
weight: 2
chapter: false
pre: " <b> 5.2.2 </b> "
---

# Create IAM Roles

We need to create an IAM Role for our Lambda function. This role gives Lambda permission to access other AWS services like S3 (for assets), SES (for emails), and RDS (for data).

## 1. Create Lambda Execution Role

### CLI
```bash
# 1. Create trust policy file
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

# 2. Create the role
aws iam create-role \
  --role-name lambda-execution-role \
  --assume-role-policy-document file://lambda-trust-policy.json

# 3. Attach standard policies
aws iam attach-role-policy \
  --role-name lambda-execution-role \
  --policy-arn arn:aws:iam::aws:policy/service-role/AWSLambdaVPCAccessExecutionRole

aws iam attach-role-policy \
  --role-name lambda-execution-role \
  --policy-arn arn:aws:iam::aws:policy/CloudWatchLogsFullAccess
```

### AWS Console
1. Open the [IAM Console](https://console.aws.amazon.com/iam).
2. Go to **Roles** → **Create role**.
3. **Trusted entity type**: AWS service.
4. **Service**: Lambda.
5. Click **Next**.
6. **Add permissions**: Search and select:
   - `AWSLambdaVPCAccessExecutionRole`
   - `CloudWatchLogsFullAccess`
7. Click **Next**.
8. **Role name**: `lambda-execution-role`.
9. Click **Create role**.

---

## 2. Add Custom Permissions

We need to give Lambda specific access to our S3 buckets and RDS.

### CLI
```bash
# 1. Create policy document
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

# 2. Attach inline policy
aws iam put-role-policy \
  --role-name lambda-execution-role \
  --policy-name lambda-custom-permissions \
  --policy-document file://lambda-custom-policy.json
```

### AWS Console
1. Go to **Roles** and select `lambda-execution-role`.
2. In the **Permissions** tab, click **Add permissions** → **Create inline policy**.
3. Select **JSON** editor and paste the policy JSON above.
4. Click **Next**.
5. **Policy name**: `lambda-custom-permissions`.
6. Click **Create policy**.
