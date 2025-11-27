---
title : "Create RDS database instance"
date : "2025-10-27"
weight : 4
chapter : false
pre : " <b> 5.4 </b> "
---

#### Preparing the EC2 Environment

**ℹ️ Information**: Before creating our database, let's prepare our EC2 instance with the necessary tools (Git and Node.js) to run our application and connect to the database.

1.  **Connect to your EC2 instance** via SSH (as done in the previous step).

2.  **Install Git**:
    Update your system and install Git to clone the application repository.
    ```bash
    sudo dnf update -y
    sudo dnf install git -y
    git --version
    ```

3.  **Install Node.js**:
    We will use a script to install Node.js (LTS version) and necessary dependencies.
    
    Create a script file:
    ```bash
    nano install_node.sh
    ```
    
    Paste the following content:
    ```bash
    #!/bin/bash
    
    # Install nvm (Node Version Manager)
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash
    . ~/.nvm/nvm.sh
    
    # Install Node.js LTS
    nvm install --lts
    nvm use --lts
    
    # Verify installation
    node -v
    npm -v
    
    # Install global development tools
    npm install -g nodemon
    
    echo "Node.js installation complete."
    ```
    
    Save and exit (`Ctrl+O`, `Enter`, `Ctrl+X`).
    
    Run the script:
    ```bash
    bash install_node.sh
    ```

#### Creating the RDS Database Instance

**ℹ️ Information**: Now we will create a MySQL database instance using Amazon RDS.

#### Step-by-Step Guide

1.  Navigate to the **Amazon RDS** console.

2.  Click **Create database**.

3.  **Choose a database creation method**: Select **Standard create**.

    ![Create RDS](/images/4/0004.png?featherlight=false&width=90pc)

4.  **Engine options**:
    - **Engine type**: Select **MySQL**.
    - **Edition**: Select **MySQL Community**.
    - **Version**: Select the latest available version (or **MySQL 8.0.x**).

5.  **Templates**:
    - Select **Free tier** (if available and applicable) or **Dev/Test** for this workshop.
    
    **💡 Pro Tip**: Selecting **Free tier** automatically hides options that would incur costs, such as Multi-AZ and Provisioned IOPS.

6.  **Settings**:
    - **DB instance identifier**: Enter a name (e.g., `workshop-db`).
    - **Master username**: `admin` (or your preferred username).
    - **Master password**: Enter a strong password and confirm it.

    **⚠️ Warning**: Do not use **Auto generate a password** unless you store it immediately. It's easier to set your own for this workshop.

    ![Create RDS](/images/4/0006.png?featherlight=false&width=90pc)

7.  **Instance configuration**:
    - **DB instance class**: Select **Burstable classes (includes t classes)** -> **db.t3.micro** (Free tier eligible).

8.  **Storage**:
    - **Storage type**: General Purpose SSD (gp2 or gp3).
    - **Allocated storage**: `20` GiB.

9.  **Connectivity**:
    - **Compute resource**: Don't connect to an EC2 compute resource.
    - **VPC**: Select your workshop VPC.
    - **DB Subnet Group**: Select the group you created in step 5.2.4.
    - **Public access**: **No** (Best practice for security).
    - **VPC security group**: Select **Choose existing** and pick the **RDS Security Group** created in step 5.2.3. Remove the `default` security group.

    **🔒 Security Note**: Ensuring Public access is **No** and using the correct Security Group prevents unauthorized internet access to your database.

    ![Create RDS](/images/4/0009.png?featherlight=false&width=90pc)

10. **Additional configuration**:
    - **Initial database name**: Enter `workshopdb` (This allows RDS to create the schema for you automatically).
    - Leave other settings as default.

11. Click **Create database**.

    ![Create RDS](/images/4/00012.png?featherlight=false&width=90pc)

#### Verifying the Database

1.  Wait for the **Status** to change from `Creating` to `Available`.
2.  Click on the **DB identifier** (`workshop-db`) to view details.
3.  Note the **Endpoint** (e.g., `workshop-db.xxxxxx.us-east-1.rds.amazonaws.com`). You will need this to connect your application.

    ![Create RDS](/images/4/00017.png?featherlight=false&width=90pc)

#### Monitoring and Maintenance

**ℹ️ Information**: RDS provides built-in tools for monitoring and maintenance.

-   **Logs & Events**: Check the **Logs & events** tab to see error logs, slow query logs, and administrative events.
-   **Maintenance & backups**: Check this tab to see your backup window and any pending maintenance updates.

**💡 Pro Tip**: Enable **Enhanced Monitoring** for granular, real-time metrics if you need to debug performance issues.
