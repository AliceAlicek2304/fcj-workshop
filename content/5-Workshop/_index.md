---
title : "Workshop: Get Started with Amazon RDS"
date : "2025-10-27"
weight : 5
chapter : false
pre: " <b> 5. </b> "
---

# Amazon Relational Database Service (Amazon RDS)

#### Overview of Amazon RDS

**ℹ️ Information**: Amazon Relational Database Service (Amazon RDS) is a managed service that allows you to deploy and manage relational databases on AWS. Amazon RDS is designed for online transaction processing (OLTP) and is best suited for structured, relational data storage requirements.

Amazon RDS provides key benefits:
- Easy replacement for traditional database instances
- Automated backups and patching during customer-defined maintenance windows
- One-click scaling, replication, and availability

![Create a VPC](/images/1/0001.png?featherlight=false&width=90pc)

#### Supported Database Engines

Amazon RDS supports the following database engines:
- Amazon Aurora
- MySQL
- MariaDB
- Oracle
- SQL Server
- PostgreSQL

**⚠️ Warning**: RDS is a managed service and you don't have root access to the underlying EC2 server. The exception is **Amazon RDS Custom**, which allows access to the underlying operating system but is only available for a limited set of DB Engines.

#### Storage Options

- **General Purpose SSD (gp3/gp2)**: Cost-effective storage providing 3 IOPS/GB baseline performance
- **Provisioned IOPS SSD (io1/io2)**: High-performance storage with customizable IOPS for I/O-intensive workloads
- **Magnetic Storage**: Legacy option with limited performance (not recommended for new deployments)

**💡 Pro Tip**: Choose General Purpose SSD for most workloads, and Provisioned IOPS only when you need consistent I/O performance for database-intensive applications.

#### High Availability and Disaster Recovery

- **Multi-AZ Deployments**: Synchronous standby replica in a different Availability Zone for automatic failover
- **Read Replicas**: Asynchronous replication for read scaling and potential disaster recovery
- **Global Databases**: Cross-region replication with fast local reads and disaster recovery capabilities

**🔒 Security Note**: Multi-AZ deployments enhance both availability and data durability, with automatic failover typically completing within 60-120 seconds.

#### Security Features

- **Encryption at rest**: Using AWS KMS keys (applies to DB instances, backups, snapshots, and replicas)
- **Network isolation**: Using Amazon VPC for network-level isolation
- **Resource-level permissions**: Using IAM policies
- **SSL/TLS encryption**: For data in transit
- **Database authentication**: Using database engine native authentication or IAM authentication

#### Scalability and Limits

- Storage can be scaled up (not down) without downtime
- Compute resources can be modified with a brief downtime during the change
- Maximum storage: 64 TiB for most engines (16 TiB for SQL Server)
- Maximum database connections: Varies by engine and instance size

**💡 Pro Tip**: Plan your initial storage carefully as you can only scale up. Consider using Aurora for more flexible scaling options.

#### Backup and Recovery

- **Automated backups**: Point-in-time recovery for up to 35 days
- **Manual snapshots**: User-initiated backups that persist until explicitly deleted
- **Snapshot export to S3**: For long-term retention or analysis

#### When to Use Amazon RDS

Amazon RDS is ideal for:
- Traditional relational database workloads
- Applications requiring SQL query capabilities
- Structured data with well-defined schemas
- OLTP workloads with predictable scaling needs

**ℹ️ Information**: For unstructured data, high-scale requirements, or specialized workloads, consider alternative AWS database services like DynamoDB, DocumentDB, or purpose-built databases.
