---
title: "Backup & Restore"
date: "2025-10-27"
weight: 6
chapter: false
pre: " <b> 5.6 </b> "
---

# Backup and Recovery Strategy

For the GameTracker application, data is our most critical asset. We need to protect:
1.  **Structured Game Data**: Stored in **Amazon RDS (SQL Server)**.
2.  **Game Assets**: Images and files stored in **Amazon S3**.

## 1. RDS Backup (SQL Server)

Amazon RDS provides two different methods for backing up your DB instances:

### A. Automated Backups
When we created the RDS instance, we enabled convenient **Automated backups**.
-   **Retention Period**: We set it to **7 days**.
-   **Function**: AWS creates a storage volume snapshot of your DB instance, backing up the entire DB instance to S3.
-   **Point-in-Time Recovery**: You can restore your database to any specific second during your retention period.

### B. Manual Snapshots
You can take a snapshot of your database at any time. Unlike automated backups, manual snapshots are kept until you explicitly delete them.

**Steps to create a Manual Snapshot:**
1.  Open [RDS Console](https://console.aws.amazon.com/rds).
2.  Go to **Databases** -> Select `gametracker-mssql`.
3.  Click **Actions** -> **Take snapshot**.
4.  Info:
    -   **Snapshot name**: `gametracker-manual-backup-v1`.
5.  Click **Take snapshot**.

![RDS Snapshot](/images/5/00019.png?featherlight=false&width=90pc)

---

## 2. S3 Data Protection

For our `gametracker-assets` bucket, we should enable **Versioning**. This allows us to preserve, retrieve, and restore every version of every object stored in the bucket.

**Steps to enable Versioning:**
1.  Open [S3 Console](https://console.aws.amazon.com/s3).
2.  Select the **gametracker-assets** bucket.
3.  Go to the **Properties** tab.
4.  Under **Bucket Versioning**, click **Edit**.
5.  Select **Enable**.
6.  Click **Save changes**.

Now, if an admin accidentally deletes or overwrites a character image, you can easily restore the previous version.

---

## 3. Restore Strategy

In case of a failure (e.g., accidental data deletion in SQL Server):
1.  Go to **RDS Console** -> **Snapshots**.
2.  Select the latest snapshot (Automated or Manual).
3.  Click **Actions** -> **Restore snapshot**.
4.  **New DB Instance Identifier**: e.g., `gametracker-mssql-restore`.
5.  Once restored and available, update your **Lambda Environment Variables** (`SPRING_DATASOURCE_URL`) to point to the new endpoint.
