---
title : "Create RDS Security Group"
date : "2025-10-27"
weight : 3
chapter : false
pre : " <b> 5.2.3 </b> "
---

#### Creating a Security Group for Amazon RDS

**ℹ️ Information**: Just like our EC2 instance, our RDS database needs a Security Group to control traffic. This security group will act as a firewall, allowing access **only** from our application servers.

#### Step-by-Step Guide

1.  In the **VPC Dashboard**, select **Security Groups** from the left navigation pane.

2.  Click **Create security group**.

    ![Create a Security Group](/images/2/0001.png?featherlight=false&width=90pc)

3.  **Basic details**:
    - **Security group name**: Enter a descriptive name (e.g., `RDS-MySQL-SG`).
    - **Description**: Enter a description (e.g., `Allow MySQL access from EC2`).
    - **VPC**: Select the same VPC as before.

4.  **Inbound rules**: Click **Add rule** to allow database connections:

    | Type | Protocol | Port Range | Source | Description |
    | :--- | :--- | :--- | :--- | :--- |
    | **MySQL/Aurora** | TCP | 3306 | **sg-xxxxxxxx** (EC2-Web-SG) | Allow MySQL access from EC2 SG |

    **🔒 Security Note**: Instead of entering an IP address (like `0.0.0.0/0`), select the **Security Group ID** of the EC2 Security Group you created in the previous step. This ensures that **only** instances belonging to that specific security group can connect to your database. This is a best practice for security.

    ![Configure Inbound Rules](/images/2/0002.png?featherlight=false&width=90pc)

5.  **Outbound rules**: Leave the default rule (Allow all traffic) unchanged.

6.  Click **Create security group**.

    ![Create the Security Group](/images/2/0003.png?featherlight=false&width=90pc)

7.  You now have a dedicated security group for your database layer.

    ![Security Group Created](/images/2/0004.png?featherlight=false&width=90pc)

**⚠️ Warning**: Never use the same Security Group for both your EC2 instances and your RDS instances. Separation of duties is key to a secure architecture.
