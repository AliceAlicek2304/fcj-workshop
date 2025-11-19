---
title : "Clean up resources"
date : "2025-10-27"
weight : 7
chapter : false
pre : " <b> 5.7 </b> "
---

#### Resource Cleanup

ℹ️ \*\*ℹ️\ Information\*\*: After completing your lab, it's important to clean up all AWS resources to avoid ongoing charges. Follow these steps to properly remove all resources created during this workshop.

#### Delete Database Resources

1. **Delete the DB subnet group**:
   - Navigate to the Amazon RDS console
   - In the navigation pane, select **Subnet groups**
   - Select the DB subnet group related to the lab
   - Choose **Delete**, then confirm by selecting **Delete** in the confirmation window

2. **Delete DB Instance**:
   - Access the RDS Management Console
   - In the left navigation bar, select **Databases**
   - Select the DB Instance related to the lab
   - Click **Actions**, then **Delete**
   - Uncheck **Create final snapshot?** and acknowledge that automated backups will no longer be available
   - Enter `delete me` in the confirmation field
   - Click **Delete**

3. **Delete DB Snapshots**:
   - In the RDS Management Console, select **Snapshots** from the navigation bar
   - Select all snapshots related to the lab
   - Click **Actions**, then **Delete snapshot**
   - Confirm by clicking **Delete**

#### Delete Network Resources

1. **Delete security groups**:
   - Open the Amazon VPC console
   - Choose **Security Groups** from the navigation pane
   - Select the security group related to the lab
   - Choose **Actions**, select **Delete security groups**, then confirm

2. **Delete NAT gateway**:
   - In the VPC console, select **NAT Gateways**
   - Select the NAT Gateway related to the lab
   - Choose **Actions**, select **Delete NAT gateway**
   - Confirm the deletion

3. **Release Elastic IP addresses**:
   - Open the Amazon EC2 console
   - Select **Elastic IPs** from the navigation pane
   - Select the Elastic IP address related to the lab
   - From **Actions**, select **Release Elastic IP addresses**
   - Confirm by choosing **Release**

4. **Delete the VPC**:
   - In the VPC console, select **Your VPCs**
   - Select the VPC you created for this lab
   - From **Actions**, select **Delete VPC**
   - On the confirmation page, enter `delete` and choose **Delete**

#### Delete Compute Resources

1. **Terminate EC2 instances**:
   - Access the EC2 Management Console
   - Select **Instances** from the navigation pane
   - Select all EC2 Instances related to the lab
   - Click **Instance state**, then **Terminate instance**
   - Confirm by clicking **Terminate**

⚠️ \*\*⚠️\ Warning\*\*: Terminating resources is permanent and cannot be undone. Ensure you have backed up any important data before proceeding with cleanup.

💡 **Pro Tip**: To verify all resources have been properly deleted, check your AWS Billing dashboard or use AWS Cost Explorer to ensure no unexpected charges appear after cleanup.

