---
title : "Create EC2 Security Group"
date : "2025-10-27"
weight : 2
chapter : false
pre : " <b> 5.2.2 </b> "
---

#### Creating a Security Group for EC2 Instances

\*\*ℹ️\ Information\*\*: Security groups act as virtual firewalls for your Amazon EC2 instances to control inbound and outbound traffic. For our RDS deployment, we need to create a security group for EC2 instances that will connect to our database.

Follow these steps to create a security group with the necessary ports:

1. Navigate to the AWS Management Console and sign in to your account.

2. In the AWS Management Console, search for and select **EC2** under services.

3. In the EC2 navigation pane, under **Network & Security**, select **Security Groups**.

4. Click the **Create security group** button.

![Create a Security Group](/images/1/0009.png?featherlight=false&width=90pc)

5. In the **Basic details** section:
   - Enter a descriptive **Security group name** (e.g., "EC2-Web-App-SG")
   - Provide a meaningful **Description** (e.g., "Security group for EC2 instances connecting to RDS")
   - Select your VPC from the dropdown menu

![Configure Security Group Details](/images/1/00010.png?featherlight=false&width=90pc)

6. In the **Inbound rules** section, click **Add rule** to configure the following access:
   - **HTTP (80)**: Select "HTTP" from the Type dropdown (automatically sets port 80)
   - **HTTPS (443)**: Select "HTTPS" from the Type dropdown (automatically sets port 443)
   - **Custom TCP (5000)**: Select "Custom TCP" and enter "5000" in the Port range field
   - **SSH (22)**: Select "SSH" from the Type dropdown (automatically sets port 22)

   **ðŸ”’ Security Note**: For production environments, restrict the source IP addresses for SSH access to only trusted IP ranges rather than allowing access from anywhere (0.0.0.0/0).

![Configure Inbound Rules](/images/1/00011.png?featherlight=false&width=90pc)

7. Review your settings and click **Create security group**.

![Create the Security Group](/images/1/00012.png?featherlight=false&width=90pc)

8. Once created, the new security group appears in your security groups list. Note the Security Group ID as you'll need it when launching EC2 instances.

![Security Group Created](/images/1/00013.png?featherlight=false&width=90pc)

**ðŸ’¡ Pro Tip**: You can modify security group rules at any time, and the changes take effect immediately. This allows you to adjust access controls as your application requirements evolve.

\*\*⚠️\ Warning\*\*: Security groups are stateful â€” if you allow inbound traffic on a specific port, the corresponding outbound response traffic is automatically allowed, regardless of outbound rules.

