# [Week 3 - Database and Security services on AWS (Youtube)](https://www.youtube.com/watch?v=Zdai0f0yf-I&t=2s)
## Table of contents
- Relational Databases on AWS
- Database Migration
- Propose-Built Databases
- DynamoDB
- Data Lake Introduction
- Shared Responsibility Model
- AWS Identity and Access Management
- AWS Organization
- AWS Single Sign-On
- Compliance and Security Center

## Relational Databases on AWS

### Amazon RDS
Managed relational database service with a choice of six popular database engines
- Easy to administer: No need for infrastructure provisioning or installing and maintaining database software
- Available and durable: Automatic Multi-AZ data replcation; automated backup, snapshots, and failover
- Highly scalable: Scale database compute and storage with a few clicks with no application downtime
- Fast and Secure: SSD storage and guaranteed provisioned I/O; data encruption at rest and in transit

#### Amazon RDS - fully managed
Spend time innovating and building new apps, not managin infrastructure
- You: Schema design, Query construction, Query optimization
- AWS:
    - Automatic fail-over
    - Backup and recovery
    - Isolation and security
    - Industry compliance
    - Push-button scaling
    - Automated patching and upgrade
    - Advanced monitoring
    - Routine maintenance

#### Monitoring RDS/Aurora databases
- Amazon CloudWatch:
    - CPU/Memory/IOPS/Network
    - Per minute metric storage in Amazon CloudWatch
- Amazon RDS Enhanced Monitoring
    - Process/Thread list
    - Per second metric storage in Amazon CloudWatch Logs
- Amazon RDS Performance Insights
    - SQL/State/User/Host ("Database Load)
    - Per second metric storage in Amazon RDS

#### Performance Insights increase productivity
Amazon RDS Performance Insights measures database load overtime
Easy to identify database bottlenecks
- Top SQL/most intensive queries
Enables problem discovery
Adjustable timeframe
- Hour, day, week, and longer
Available for all Amazon RDS database engines

#### RDS Features
##### Multi-AZ deployments
Fault tolerance across multiple data centers
- Automatic failover
- Synchronous replication
- Anabled with one click

![Multi-AZ deployments](assets/week3/multi_az_deployments.png)
##### Read Replicas
RDS for MySQL, PostgreSQL, MariaDB, and Oracle
- Relieve pressure on your master node with additional read capacity
- Bring data close to your applications in different regions
- Promote a read replica to a master for faster in the event of disaster

![Read scaling and disaster recovery](assets/week3/read_replica.png)

Read replica can promote to become primary in-case we need, it is cross region also.

##### Automated backups
- Schedule daily volume backup of entire instance
- Archive database change logs
- 35-day maximum retention
- Minimal impact on database performance
- Taken from standby when runing Multi-AZ

*Every day during your backup window, RDS creates a storage volume snapshop of your instance*

*Every five minutes, RDS backs up the transaction logs of your database*

##### Database snapshots
- Always incremental
- Amazon S3 -> 99.9999999999% durability
- Supports encryption
- Copy across accounts, across regions

![Backups of your entire DB instance in Amazon S3](assets/week3/database_snapshots.png)

### Amazon Aurora

*You asked for a cost-effective, enterprise database...*

So, we designed Aurora - enterprise database at open source price, delivered as a managed service
- Speed and availability of high-end commercial databases
- Simplicity and cost-effectiveness of open source databases
- Drop-in compatibility with MySQL and PostgreSQL
- Simple pay as you go pricing

*Amazon Aurora is fast... up to 5x the throughput of MySQL; 3x the throughput of PostgreSQL*

#### Traditional Database Architecture
Databases are all about I/O...

Design principles over the last 40+ years:
- Increase I/O bandwidth
- Decrease number of I/Os consumed

#### Scale-out, distributed, multi-tenant storage architecture
- Purpose-built log-structured distributed storage
- Storage volume is triped across hundreds of storage nodes
- Storage nodes with locally attached SSDs
- Continuous backup to Amazon S3

![Aurora Architecture](assets/week3/aurora_architecture.png)

#### Tolerating compute failures
- Any reader node can be promoted to writer/primary
- Failed instances/nodes will be replaced after failover and come online as readers

![Tolerating Compute Failures](assets/week3/tolerating_compute_failures.png)

## Database Migration