---
title : "Create RDS Security Group"
date : "2025-10-27"
weight : 3
chapter : false
pre : " <b> 5.2.3 </b> "
---

#### Creating a Security Group for Amazon RDS

\*\*ℹ️ Information\*\*: Security groups act as virtual firewalls for your Amazon RDS instances, controlling inbound and outbound traffic at the instance level. Each security group contains a set of rules that filter traffic based on protocol, port, and source or destination.

Follow these steps to create a dedicated security group for your Amazon RDS database instance:

1. Navigate to the Amazon VPC console and select **Security Groups** from the navigation pane.

2. Click **Create Security Group** to create a new security group specifically for your RDS database instance.

3. In the **Basic details** section:
   - Enter a descriptive **Security group name** (e.g., "RDS-MySQL-SG")
   - Provide a meaningful **Description** (e.g., "Security group for RDS MySQL database instances")
   - Select your VPC from the dropdown menu

![Create a Security Group](/images/2/0001.png?featherlight=false&width=90pc)

4. Ensure the VPC you created earlier is selected to associate the security group with your network environment.

5. Configure **Inbound rules** to control which traffic sources can access your database:
   - Select **MySQL/Aurora** from the Type dropdown (automatically sets port 3306)
   - For **Source**, select the security group ID of your EC2 instances that need to connect to the database
   
   **🔒 Security Note**: Specifying the EC2 security group as the source rather than an IP range ensures only instances with that security group can connect to your database, enhancing security.

![Configure Inbound Rules](/images/2/0002.png?featherlight=false&width=90pc)

6. Review your settings and click **Create Security Group** to complete the process.

![Create the Security Group](/images/2/0003.png?featherlight=false&width=90pc)

**💡 Pro Tip**: You can modify security group rules at any time, and the changes take effect immediately. This allows you to adjust access controls as your application requirements evolve.

\*\*⚠️ Warning\*\*: It is a best practice to use separate security groups for your RDS instances and EC2 instances. This separation provides better security isolation and makes it easier to manage permissions for each resource type independently.

![Security Group Created](/images/2/0004.png?featherlight=false&width=90pc)

