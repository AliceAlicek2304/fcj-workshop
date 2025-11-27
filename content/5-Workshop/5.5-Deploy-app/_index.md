---
title : "Application Deployment"
date : "2025-10-27"
weight : 5
chapter : false
pre : " <b> 5.5 </b> "
---

#### Deploying the Node.js Application

**ℹ️ Information**: Now that our infrastructure (EC2 and RDS) is ready, we will deploy our sample Node.js application.

#### Step 1: Clone the Repository

1.  Connect to your EC2 instance via SSH (if not already connected).
2.  Clone the workshop repository:

    ```bash
    git clone https://github.com/AWS-First-Cloud-Journey/AWS-FCJ-Management
    cd AWS-FCJ-Management
    ```

#### Step 2: Install Dependencies

1.  Initialize the project and install required packages:

    ```bash
    npm install
    ```

#### Step 3: Configure Database Connection

1.  Create a `.env` file to store your database credentials:

    ```bash
    nano .env
    ```

2.  Paste the following content, replacing the placeholders with your actual RDS details:

    ```env
    DB_HOST=your-rds-endpoint.us-east-1.rds.amazonaws.com
    DB_USER=admin
    DB_PASSWORD=your-password
    DB_NAME=workshopdb
    DB_PORT=3306
    ```

    -   **DB_HOST**: The Endpoint you copied from the RDS console.
    -   **DB_USER**: The Master username you set (e.g., `admin`).
    -   **DB_PASSWORD**: The Master password you set.
    -   **DB_NAME**: The database name (e.g., `workshopdb`).

3.  Save and exit (`Ctrl+O`, `Enter`, `Ctrl+X`).

#### Step 4: Initialize the Database

**ℹ️ Information**: We need to create the necessary tables for our application. We will use a simple script or SQL commands.

1.  Create a file named `init_db.js` (or use the provided SQL script if available in the repo). If you need to manually create the table, you can connect using a MySQL client or use a Node.js script like this:

    ```javascript
    const mysql = require('mysql');
    require('dotenv').config();

    const connection = mysql.createConnection({
      host: process.env.DB_HOST,
      user: process.env.DB_USER,
      password: process.env.DB_PASSWORD,
      database: process.env.DB_NAME
    });

    connection.connect();

    const createTableQuery = `
      CREATE TABLE IF NOT EXISTS users (
        id INT AUTO_INCREMENT PRIMARY KEY,
        name VARCHAR(255) NOT NULL,
        email VARCHAR(255) NOT NULL,
        created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
      )
    `;

    connection.query(createTableQuery, (error, results, fields) => {
      if (error) throw error;
      console.log('Table created successfully');
    });

    connection.end();
    ```

    *Note: The actual application might have its own migration script. Ensure you follow the repository's specific instructions if they differ.*

#### Step 5: Start the Application

1.  Start the application using `npm`:

    ```bash
    npm start
    ```

    You should see a message indicating the server is running (e.g., `Server running on port 3000` or `5000`).

#### Step 6: Verify Deployment

1.  Open your web browser.
2.  Navigate to `http://<EC2-Public-IP>:5000` (or the port your app uses).
3.  You should see your application running and connected to the RDS database.

    ![App Running](/images/5/00011.png?featherlight=false&width=90pc)

**💡 Pro Tip**: If you cannot access the application, verify that your **EC2 Security Group** allows inbound traffic on the application port (e.g., 5000) from your IP address.
