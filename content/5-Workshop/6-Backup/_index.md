---
title : "Backup and Restore"
date : "2025-10-27"
weight : 6
chapter : false
pre : " <b> 5.6 </b> "
---

#### Understanding Amazon RDS Backup and Restore

**ℹ️ Information**: Amazon RDS provides automated backups and allows manual snapshots to ensure your database data is protected and can be recovered when needed. These capabilities are essential for disaster recovery planning and maintaining business continuity.

#### Monitoring Backup Status

1.  **Access Monitoring**:
    -   Navigate to the **Databases** section in the AWS Management Console.
    -   Select your target DB instance.
    -   Click on the **Monitoring** tab to view performance metrics.

    ![AWS RDS Monitoring](/images/5/00014.png?featherlight=false&width=90pc)

#### Managing Backups

1.  **View Backup Details**:
    -   Select your DB instance.
    -   Navigate to the **Maintenance & backups** tab.
    -   Here you can view both automated and manual backup information and configure backup settings.

    ![AWS RDS Backup](/images/5/00019.png?featherlight=false&width=90pc)

2.  **View Snapshots**:
    -   In the left navigation pane, click **Snapshots**.
    -   You will see a list of all manual and automated snapshots.

    ![Snapshot Information](/images/5/00020.png?featherlight=false&width=90pc)

#### Restoring from a DB Snapshot

**ℹ️ Information**: Restoring a snapshot creates a **new** DB instance. It does not overwrite the existing one.

1.  **Select Snapshot**:
    -   Choose the DB snapshot you want to restore.
    -   Click **Actions** > **Restore snapshot**.

    ![Restore Snapshot](/images/5/00021.png?featherlight=false&width=90pc)

2.  **Configure New Instance**:
    -   **DB instance identifier**: Enter a unique name for the new instance (e.g., `workshop-db-restore`).
    -   **Instance specifications**: Select the instance class (e.g., `db.t3.micro`).
    -   **Connectivity**: Select the same VPC and Subnet Group as your original instance.
    -   **Security**: Choose the correct Security Group.

    **💡 Pro Tip**: When restoring for testing, you can choose a smaller instance class to save costs.

    ![Restore Settings](/images/5/00022.png?featherlight=false&width=90pc)

3.  **Initiate Restore**:
    -   Click **Restore DB instance**.

    **⚠️ Warning**: The restore process creates a completely new database instance with a new endpoint. You must update your application's connection string to point to this new endpoint.

    ![Restore Complete](/images/5/00027.png?featherlight=false&width=90pc)

4.  **Verify**:
    -   Wait for the status to change to **Available**.
    -   Test connectivity to the new instance.

    ![Verify Restore](/images/5/00028.png?featherlight=false&width=90pc)
