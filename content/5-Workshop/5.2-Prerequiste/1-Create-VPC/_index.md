---
title : "Create a VPC"
date : "2025-10-27"
weight : 1
chapter : false
pre : " <b> 5.2.1 </b> "
---

#### Creating a VPC with Subnets and Associated Resources

**ℹ️ Information**: Amazon Virtual Private Cloud (Amazon VPC) is your private network in the cloud. It allows you to launch AWS resources into a virtual network that you define, giving you complete control over your network environment.

We will use the **VPC and more** wizard to create our VPC, subnets, route tables, and internet gateway in a single workflow.

#### Step-by-Step Guide

1.  Open the Amazon VPC console at [https://console.aws.amazon.com/vpc/](https://console.aws.amazon.com/vpc/).

    ![Create a VPC](/images/1/0001.png?featherlight=false&width=90pc)

2.  On the VPC dashboard, choose **Create VPC**.

3.  Under **Resources to create**, select **VPC and more**. This option automatically provisions related resources like subnets and route tables.

    ![Create a VPC](/images/1/0002.png?featherlight=false&width=90pc)

4.  **Name tag auto-generation**: Enter a name for your project (e.g., `workshop-vpc`). This will be used as a prefix for all created resources.

5.  **IPv4 CIDR block**: Keep the default (e.g., `10.0.0.0/16`) or enter your preferred range.

6.  **Availability Zones (AZs)**: Select **2**. This is critical for High Availability and Multi-AZ deployments.

    ![Create a VPC](/images/1/0003.png?featherlight=false&width=90pc)

7.  **Number of public subnets**: Select **2**. These will host resources that need direct internet access (like a bastion host or load balancer).

8.  **Number of private subnets**: Select **2**. These will host your RDS database instances, keeping them secure from the public internet.

    **🔒 Security Note**: Always place your database instances in private subnets.

9.  **NAT gateways**: Select **1 per AZ** or **1 in 1 AZ** depending on your cost preference. For this workshop, **None** or **1 in 1 AZ** is sufficient if you need outbound internet access for private instances (e.g., for updates).

    **💡 Pro Tip**: In a production environment, deploying a NAT Gateway in each AZ ensures high availability but incurs higher costs.

10. **VPC endpoints**: Leave as **None** for this workshop.

11. **DNS options**: Ensure **Enable DNS hostnames** and **Enable DNS resolution** are checked. These are required for RDS to function correctly with public access (if needed) and for easier internal resolution.

12. Review the **Preview** pane to visualize your network architecture.

13. Click **Create VPC**.

    ![Create a VPC](/images/1/0004.png?featherlight=false&width=90pc)

    ![Create a VPC](/images/1/0005.png?featherlight=false&width=90pc)

#### Configuring Public IP Assignment (Optional)

**ℹ️ Information**: By default, instances in non-default subnets do not get public IP addresses. If you want instances in your **Public Subnets** to automatically get a public IP, follow these steps:

1.  Go to **Subnets** in the left navigation pane.
2.  Select one of your **Public Subnets**.
3.  Click **Actions** > **Edit subnet settings**.

    ![Create a VPC](/images/1/0007.png?featherlight=false&width=90pc)

4.  Check **Enable auto-assign public IPv4 address**.
5.  Click **Save**.
6.  Repeat for your other Public Subnet.

    ![Create a VPC](/images/1/0008.png?featherlight=false&width=90pc)

**⚠️ Warning**: Never enable auto-assign public IP for your **Private Subnets** where your database resides.
