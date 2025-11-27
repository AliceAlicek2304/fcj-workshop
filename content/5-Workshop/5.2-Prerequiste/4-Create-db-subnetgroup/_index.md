---
title : "Create DB Subnet Group"
date : "2025-10-27"
weight : 4
chapter : false
pre : " <b> 5.2.4 </b> "
---

#### Creating a DB Subnet Group for Amazon RDS

**ℹ️ Information**: A **DB Subnet Group** is a collection of subnets (typically private) that you designate for your RDS instances. It tells RDS which subnets and IP ranges it can use in your VPC.

**⚠️ Warning**: To enable Multi-AZ deployments (High Availability), your DB Subnet Group **must** include subnets in at least **two different Availability Zones**.

#### Step-by-Step Guide

1.  Navigate to the **Amazon RDS** console.

2.  In the left navigation pane, select **Subnet groups**.

3.  Click **Create DB Subnet Group**.

    ![Create DB Subnet Group](/images/2/0005.png?featherlight=false&width=90pc)

4.  **Subnet group details**:
    - **Name**: Enter a name (e.g., `rds-subnet-group`).
    - **Description**: Enter a description (e.g., `Subnet group for RDS`).
    - **VPC**: Select your VPC.

    ![Configure DB Subnet Group Details](/images/2/0006.png?featherlight=false&width=90pc)

5.  **Add subnets**:
    - **Availability Zones**: Select the Availability Zones where you created your private subnets (e.g., `us-east-1a` and `us-east-1b`).
    - **Subnets**: Select the specific **Private Subnet IDs** associated with those AZs.

    **🔒 Security Note**: Always select **Private Subnets** for your database to ensure it is not directly accessible from the internet.

6.  Click **Create**.

    ![Add Subnets to DB Subnet Group](/images/2/0007.png?featherlight=false&width=90pc)

7.  Your DB Subnet Group is now ready.

    ![DB Subnet Group Created](/images/2/0008.png?featherlight=false&width=90pc)

**💡 Pro Tip**: If you are using AWS Local Zones, you can also include them here to extend your database closer to your end-users.
