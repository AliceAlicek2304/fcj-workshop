---
title : "Create EC2 instance"
date : "2025-10-27"
weight : 3
chapter : false
pre : " <b> 5.3 </b> "
---

#### Creating an EC2 Instance

**ℹ️ Information**: Amazon EC2 (Elastic Compute Cloud) provides scalable computing capacity in the AWS Cloud. It allows you to launch virtual servers (instances) in minutes, eliminating the need to invest in upfront hardware.

In this step, we will launch a Linux EC2 instance that will serve as our application server (or bastion host) to connect to our RDS database.

#### Step-by-Step Guide

1.  **Access the Console**: Open the [Amazon EC2 console](https://console.aws.amazon.com/ec2/).

2.  **Launch Instance**: On the dashboard, click the orange **Launch instance** button.

    ![Create a VPC](/images/3/0001.png?featherlight=false&width=90pc)

3.  **Name and Tags**:
    - **Name**: Enter a descriptive name (e.g., `Workshop-Web-Server`).

    ![Create a VPC](/images/3/0002.png?featherlight=false&width=90pc)

4.  **Application and OS Images (AMI)**:
    - **Quick Start**: Select **Amazon Linux**.
    - **AMI**: Select **Amazon Linux 2023 AMI** (Free tier eligible).

    **💡 Pro Tip**: Always look for the "Free tier eligible" tag to avoid unexpected costs during learning or testing.

    ![Create a VPC](/images/3/0003.png?featherlight=false&width=90pc)

5.  **Instance Type**:
    - Select **t2.micro** (or **t3.micro** if t2 is unavailable in your region).

    **ℹ️ Information**: These instance types are low-cost and often covered by the AWS Free Tier.

    ![Create a VPC](/images/3/0004.png?featherlight=false&width=90pc)

6.  **Key Pair (Login)**:
    - Select the **Key pair** you created earlier.

    **⚠️ Warning**: Do not proceed without a key pair. You will not be able to SSH into your instance without it.

    ![Create a VPC](/images/3/0005.png?featherlight=false&width=90pc)

7.  **Network Settings**:
    - Click **Edit**.
    - **VPC**: Select your workshop VPC.
    - **Subnet**: Select a **Public Subnet**.
    - **Auto-assign Public IP**: Ensure this is **Enabled**.
    - **Firewall (security groups)**: Select **Select existing security group**.
    - Choose the **EC2 Security Group** you created in step 5.2.2.

    **🔒 Security Note**: By reusing the security group we created earlier, we ensure our instance has exactly the permissions it needs—no more, no less.

    ![Create a VPC](/images/3/0006.png?featherlight=false&width=90pc)
    ![Create a VPC](/images/3/0007.png?featherlight=false&width=90pc)

8.  **Launch**:
    - Review your summary.
    - Click **Launch instance**.

    ![Create a VPC](/images/3/0008.png?featherlight=false&width=90pc)

9.  **Verify**:
    - Click **View all instances**.
    - Wait for the **Instance state** to change to `Running` and **Status check** to pass.

    **💡 Pro Tip**: If you don't see the Public DNS column, click the settings gear icon and enable **Public IPv4 DNS**.

    ![Create a VPC](/images/3/0009.png?featherlight=false&width=90pc)
    ![Create a VPC](/images/3/00010.png?featherlight=false&width=90pc)

#### Connecting via SSH (MobaXterm)

**ℹ️ Information**: MobaXterm is a powerful terminal for Windows that makes SSH connections easy.

1.  **Download & Install**: Get MobaXterm from the [official website](https://mobaxterm.mobatek.net/download-home-edition.html).

2.  **Create Session**:
    - Click **Session** > **SSH**.
    - **Remote host**: Enter your EC2 instance's **Public IPv4 DNS**.
    - **Specify username**: Enter `ec2-user`.
    - **Port**: `22`.

3.  **Authentication**:
    - Go to the **Advanced SSH settings** tab.
    - Check **Use private key**.
    - Browse and select your `.pem` key file.

    ![Create a VPC](/images/3/00011.png?featherlight=false&width=90pc)

4.  **Connect**:
    - Click **OK**.
    - You should now be connected to your Linux server!

    ![Create a VPC](/images/3/00012.png?featherlight=false&width=90pc)

**🔒 Security Note**: Keep your `.pem` key file secure. Never share it or commit it to public repositories.
