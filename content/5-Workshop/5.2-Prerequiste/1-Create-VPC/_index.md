---
title : "Create a VPC"
date : "2025-10-27"
weight : 1
chapter : false
pre : " <b> 5.2.1 </b> "
---

#### Creating a VPC with Subnets and Associated Resources

\*\*ℹ️\ Information\*\*: Amazon Virtual Private Cloud (Amazon VPC) enables you to launch AWS resources into a virtual network that you've defined. This virtual network closely resembles a traditional network in your own data center, with the benefits of using the scalable infrastructure of AWS.

Follow these steps to create a VPC with all necessary components for your Amazon RDS deployment:

1. Open the Amazon VPC console at [https://console.aws.amazon.com/vpc/](https://console.aws.amazon.com/vpc/).

![Create a VPC](/images/1/0001.png?featherlight=false&width=90pc)

2. On the VPC dashboard, choose **Create VPC**.

3. For **Resources to create**, select **VPC and more** to create a complete VPC environment.

![Create a VPC](/images/1/0002.png?featherlight=false&width=90pc)

4. Configure the **Name tag auto-generation** option based on your preference. This allows AWS to automatically create consistent naming for all VPC resources.

5. Enter an IPv4 CIDR block range for your VPC (e.g., 10.0.0.0/16). This defines the IP address range available within your VPC.

6. (Optional) To enable IPv6 support, select **IPv6 CIDR block** and choose an Amazon-provided IPv6 range.

7. Select the appropriate **Tenancy** option:
   - **Default**: EC2 instances use the tenancy attribute specified during launch
   - **Dedicated**: All EC2 instances run on hardware dedicated to your account

   **ðŸ’¡ Pro Tip**: Most workloads should use Default tenancy for cost efficiency. Only select Dedicated when you have specific compliance or licensing requirements.

8. For **Number of Availability Zones (AZs)**, select at least two AZs for high availability.

![Create a VPC](/images/1/0003.png?featherlight=false&width=90pc)

9. Configure your **Number of public subnets** and **Number of private subnets**. For Amazon RDS deployments, you'll typically need private subnets for your database instances and public subnets for resources that need internet access.

   **ðŸ”’ Security Note**: Place your RDS instances in private subnets to enhance security by preventing direct internet access to your databases.

10. (Optional) If resources in private subnets need internet access, configure **NAT gateways** in each AZ where you have resources requiring outbound connectivity.

    **ðŸ’¡ Pro Tip**: For production environments, deploy NAT gateways in each AZ to eliminate cross-AZ dependencies and improve fault tolerance.

11. (Optional) For IPv6 outbound connectivity from private subnets, select **Yes** for **Egress-only Internet Gateway**.

12. (Optional) To enable private access to Amazon S3, select **VPC endpoints, S3 Gateway**. This creates a gateway endpoint that allows resources in your VPC to access S3 without using the public internet.

13. For **DNS options**, the default settings enable both DNS resolution and DNS hostnames, which are recommended for most deployments.

14. (Optional) Add tags to your VPC by expanding **Additional tags** and entering key-value pairs.

15. Review the **Preview** pane to see a visual representation of the VPC architecture you've configured.

16. Choose **Create VPC** to provision all the configured resources.

![Create a VPC](/images/1/0004.png?featherlight=false&width=90pc)

![Create a VPC](/images/1/0005.png?featherlight=false&width=90pc)

#### Configuring Public IP Address Assignment for Subnets

\*\*ℹ️\ Information\*\*: The auto-assign public IPv4 address setting determines whether instances launched in a subnet automatically receive public IP addresses. For RDS deployments, your database subnets should typically have this setting disabled.

To modify the public IP address assignment behavior for a subnet:

1. Open the Amazon VPC console at [https://console.aws.amazon.com/vpc/](https://console.aws.amazon.com/vpc/).

2. In the navigation pane, choose **Subnets**.

![Create a VPC](/images/1/0006.png?featherlight=false&width=90pc)

3. Select your subnet and choose **Actions**, then **Edit subnet settings**.

![Create a VPC](/images/1/0007.png?featherlight=false&width=90pc)

4. Configure the **Auto-assign public IPv4 address** setting:
   - **Checked**: Instances launched in this subnet automatically receive a public IPv4 address
   - **Unchecked**: Instances launched in this subnet do not receive a public IPv4 address unless specifically requested during launch

   **ðŸ”’ Security Note**: For subnets that will host your RDS instances, ensure this setting is unchecked to prevent accidental public IP assignment.

5. Choose **Save** to apply your changes.

![Create a VPC](/images/1/0008.png?featherlight=false&width=90pc)

\*\*⚠️\ Warning\*\*: Default subnets have auto-assign public IPv4 addresses enabled by default. Always verify this setting when using default subnets for database deployments.

