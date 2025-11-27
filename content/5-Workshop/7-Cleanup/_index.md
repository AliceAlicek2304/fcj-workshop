---
title : "Clean up resources"
date : "2025-10-27"
weight : 7
chapter : false
pre : " <b> 5.7 </b> "
---

#### Resource Cleanup

**ℹ️ Information**: To avoid unexpected charges, it is crucial to clean up all resources created during this workshop. We will delete resources in the reverse order of their creation.

#### Step 1: Delete RDS Resources

1.  **Delete RDS Instance**:
    -   Go to the **Amazon RDS** console > **Databases**.
    -   Select your database instance (e.g., `workshop-db`).
    -   Click **Actions** > **Delete**.
    -   Uncheck **Create final snapshot** and check **I acknowledge...**.
    -   Type `delete me` and click **Delete**.

2.  **Delete DB Subnet Group**:
    -   Go to **Subnet groups**.
    -   Select your group (e.g., `rds-subnet-group`).
    -   Click **Delete**.

#### Step 2: Terminate EC2 Instance

1.  **Terminate Instance**:
    -   Go to the **Amazon EC2** console > **Instances**.
    -   Select your instance (e.g., `Workshop-Web-Server`).
    -   Click **Instance state** > **Terminate instance**.
    -   Click **Terminate**.

#### Step 3: Delete Network Resources

1.  **Delete Security Groups**:
    -   Go to the **VPC** console > **Security Groups**.
    -   Select the **RDS Security Group** and delete it.
    -   Select the **EC2 Security Group** and delete it.

    **💡 Pro Tip**: You must delete the RDS Security Group first because the EC2 Security Group might reference it (or vice versa depending on your rules). If you get a dependency error, check your Inbound/Outbound rules.

2.  **Delete VPC**:
    -   Go to **Your VPCs**.
    -   Select your workshop VPC.
    -   Click **Actions** > **Delete VPC**.
    -   Type `delete` and confirm.

    **ℹ️ Information**: Deleting the VPC will automatically delete associated subnets, route tables, and internet gateways.

#### Verification

1.  Check your **Billing Dashboard** the next day to ensure no active resources remain.
