---
title : "Create EC2 Security Group"
date : "2025-10-27"
weight : 2
chapter : false
pre : " <b> 5.2.2 </b> "
---

#### Creating a Security Group for EC2 Instances

**ℹ️ Information**: A Security Group acts as a virtual firewall for your EC2 instances to control incoming and outgoing traffic. In this step, we will create a security group that allows traffic to our web application.

#### Step-by-Step Guide

1.  Navigate to the **EC2 Dashboard** in the AWS Management Console.

2.  In the left navigation pane, under **Network & Security**, select **Security Groups**.

3.  Click **Create security group**.

    ![Create a Security Group](/images/1/0009.png?featherlight=false&width=90pc)

4.  **Basic details**:
    - **Security group name**: Enter a descriptive name (e.g., `EC2-Web-SG`).
    - **Description**: Enter a description (e.g., `Allow Web and SSH access`).
    - **VPC**: Select the VPC you created in the previous step.

    ![Configure Security Group Details](/images/1/00010.png?featherlight=false&width=90pc)

5.  **Inbound rules**: Click **Add rule** to allow the following traffic:

    | Type | Protocol | Port Range | Source | Description |
    | :--- | :--- | :--- | :--- | :--- |
    | **HTTP** | TCP | 80 | 0.0.0.0/0 | Allow HTTP access from anywhere |
    | **HTTPS** | TCP | 443 | 0.0.0.0/0 | Allow HTTPS access from anywhere |
    | **Custom TCP** | TCP | 5000 | 0.0.0.0/0 | Allow access to application port |
    | **SSH** | TCP | 22 | My IP | Allow SSH access only from your IP |

    **🔒 Security Note**: For SSH (Port 22), always select **My IP** as the source to restrict administrative access to your current location only. Never open SSH to `0.0.0.0/0` in a production environment.

    ![Configure Inbound Rules](/images/1/00011.png?featherlight=false&width=90pc)

6.  **Outbound rules**: Leave the default rule (Allow all traffic) unchanged.

7.  Click **Create security group**.

    ![Create the Security Group](/images/1/00012.png?featherlight=false&width=90pc)

8.  Note the **Security Group ID** (e.g., `sg-xxxxxxxx`), as you will need it later.

    ![Security Group Created](/images/1/00013.png?featherlight=false&width=90pc)

**💡 Pro Tip**: Security Groups are **stateful**. This means if you allow an inbound request, the response is automatically allowed to flow back out, regardless of outbound rules.
