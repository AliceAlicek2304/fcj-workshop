---
title : "Create EC2 instance"
date : "2025-10-27"
weight : 3
chapter : false
pre : " <b> 5.3 </b> "
---

#### Creating an EC2 Instance

â„¹ï¸ \*\*ℹ️\ Information\*\*: Amazon EC2 (Elastic Compute Cloud) provides scalable computing capacity in the AWS Cloud, eliminating the need to invest in hardware upfront.

To create a Linux EC2 instance using the AWS Management Console, follow these instructions. This guide helps you quickly launch your first instance with essential configurations. For advanced options, refer to the [Launch Instance documentation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html).

#### Access the AWS Console

1. Open a web browser and navigate to the Amazon EC2 console at [https://console.aws.amazon.com/ec2/](https://console.aws.amazon.com/ec2/).

#### Launch Your Instance

1. On the EC2 console dashboard, locate the **Launch instance** box, select **Launch instance**, then choose **Launch instance** from the dropdown menu.

   ![Create a VPC](/images/3/0001.png?featherlight=false&width=90pc)

#### Configure Instance Details

1. Under the **Name and tags** section, enter a descriptive name for your instance.

   ![Create a VPC](/images/3/0002.png?featherlight=false&width=90pc)

2. Under **Application and OS Images (Amazon Machine Image)**, configure the following:
   - Select **Quick Start**, then choose **Amazon Linux**
   - From the **Amazon Machine Image (AMI)** options, select an HVM version of **Amazon Linux 2023**
   
   ðŸ’¡ **Pro Tip**: Look for AMIs marked as **Free tier eligible** to avoid unexpected charges if you're using the AWS Free Tier.

   ![Create a VPC](/images/3/0003.png?featherlight=false&width=90pc)

3. Under **Instance type**, select **t2.micro** (pre-selected by default).
   
   â„¹ï¸ \*\*ℹ️\ Information\*\*: The **t2.micro** instance type qualifies for the AWS Free Tier. In regions where **t2.micro** isn't available, you can use **t3.micro** under the Free Tier. For more details, see [AWS Free Tier](https://aws.amazon.com/free/).

   ![Create a VPC](/images/3/0004.png?featherlight=false&width=90pc)

4. Under **Key pair (login)**, select the key pair you created during your AWS setup.

   âš ï¸ \*\*⚠️\ Warning\*\*: Do not select **Proceed without a key pair (Not recommended)**. Without a key pair, you won't be able to connect to your instance.

   ![Create a VPC](/images/3/0005.png?featherlight=false&width=90pc)

5. Under **Network settings**, click **Edit** and configure your security group:
   - You can use the auto-created security group, or
   - Select **Select existing security group** and choose a security group you created previously

   ðŸ”’ **Security Note**: Security groups act as virtual firewalls that control inbound and outbound traffic to your instance. Ensure your security group allows SSH access (port 22) from your IP address only.

   ![Create a VPC](/images/3/0006.png?featherlight=false&width=90pc)

   ![Create a VPC](/images/3/0007.png?featherlight=false&width=90pc)

#### Launch and Verify Your Instance

1. Review the instance configuration summary in the **Summary panel**.
2. When ready, click **Launch instance**.

   ![Create a VPC](/images/3/0008.png?featherlight=false&width=90pc)

3. On the confirmation page, click **View all instances** to return to the EC2 console.
4. Monitor the instance status on the Instances screen:
   - Initial state: **pending**
   - Running state: **running** (with assigned public DNS name)
   
   ðŸ’¡ **Pro Tip**: If the **Public IPv4 DNS** column is hidden, click the gear icon (Settings) in the upper right corner, enable **Public IPv4 DNS**, and click **Confirm**.

5. Wait for the instance to pass all status checks before attempting to connect.

   ![Create a VPC](/images/3/0009.png?featherlight=false&width=90pc)

   ![Create a VPC](/images/3/00010.png?featherlight=false&width=90pc)

#### Connecting to Your EC2 Instance via SSH Using MobaXterm

â„¹ï¸ \*\*ℹ️\ Information\*\*: MobaXterm is an enhanced terminal for Windows with an X11 server, tabbed SSH client, and various network tools.

Follow these steps to connect to your EC2 instance using MobaXterm:

#### Install MobaXterm

1. Download MobaXterm from the official website: [MobaXterm Website](https://mobaxterm.mobatek.net/download-home-edition.html)
2. Install the application on your computer

#### Configure SSH Connection

1. Launch MobaXterm
2. Click the **Session** icon in the upper-left corner
3. In the configuration window, enter:
   - **Remote Host**: Your EC2 instance's public IP address or DNS name
   - **Port**: 22 (default SSH port)
   - **Username**: The default user for your AMI (typically **ec2-user** for Amazon Linux)
   - **Advanced SSH settings**: Browse and select your private key file (.pem)

   ![Create a VPC](/images/3/00011.png?featherlight=false&width=90pc)

#### Connect to Your Instance

1. Click **OK** to save the configuration
2. Click the connect icon to establish an SSH connection

ðŸ”’ **Security Note**: Ensure your private key file (.pem) has restricted permissions. On Windows, verify the file is not accessible to other users.

#### Successful Connection

Once connected, you'll have terminal access to your EC2 instance and can begin managing your server.

![Create a VPC](/images/3/00012.png?featherlight=false&width=90pc)

