---
title : "Create DB Subnet Group"
date : "2025-10-27"
weight : 4
chapter : false
pre : " <b> 5.2.4 </b> "
---

#### Creating a DB Subnet Group for Amazon RDS

\*\*ℹ️\ Information\*\*: A DB subnet group is a collection of subnets that you designate for your Amazon RDS database instances within a VPC. DB subnet groups enable you to specify particular subnets and IP ranges where Amazon RDS can deploy database instances, ensuring proper network isolation and availability.

Follow these steps to create a DB subnet group:

1. Navigate to the AWS Management Console and sign in to your account.

2. Search for and select **RDS** under services.

3. In the navigation pane, select **Subnet groups**.

4. Click **Create DB Subnet Group**.

![Create DB Subnet Group](/images/2/0005.png?featherlight=false&width=90pc)

5. In the **Create DB Subnet Group** page, configure the basic details:
   - Enter a descriptive **Name** for your subnet group (e.g., "rds-subnet-group")
   - Provide a meaningful **Description** (e.g., "Subnet group for RDS instances")
   - Select the **VPC** you created earlier from the dropdown menu

![Configure DB Subnet Group Details](/images/2/0006.png?featherlight=false&width=90pc)

6. In the **Add subnets** section:
   - Select at least two different **Availability Zones** to enable Multi-AZ deployments
   - Choose the appropriate **Subnets** from each Availability Zone (typically private subnets for production databases)

   **ðŸ”’ Security Note**: For enhanced security, place your RDS instances in private subnets that don't have direct internet access.

7. Click **Create** to create your DB subnet group.

![Add Subnets to DB Subnet Group](/images/2/0007.png?featherlight=false&width=90pc)

\*\*⚠️\ Warning\*\*: A DB subnet group must include subnets in at least two different Availability Zones to support Multi-AZ deployments. Without this configuration, you won't be able to enable the Multi-AZ feature for your RDS instances.

**ðŸ’¡ Pro Tip**: If you've enabled AWS Local Zones in your account, you can also select an Availability Zone group on the Create DB Subnet Group page. In this case, select the Availability Zone group, the corresponding Availability Zones, and appropriate subnets.

After creation, your new DB subnet group will appear in the list of DB subnet groups in the RDS console. You can select it to view detailed information, including all associated subnets, in the details panel at the bottom of the window.

![DB Subnet Group Created](/images/2/0008.png?featherlight=false&width=90pc)

