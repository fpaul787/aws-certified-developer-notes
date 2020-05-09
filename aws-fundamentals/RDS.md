# Relational Database Service

## Relational Database
A relational database is a collection of data items with predefined relationships between
them. These items are organized as a set of tables with columns and rows. Tables store
information about the objects to be represented in the database. Each column in a table holds certain data, and a field stores the actual value of an attribute. The rows in the table
represent a collection of related values of one object or entity. Each row in a table contains
a unique identifier called a primary key, and rows among multiple tables can be linked by
using foreign keys. You can access data in many different ways without reorganizing the
database tables.

#### Advantage of Managed Database
* Hardware provisioning
* Setup and configuration
* Throughput capacity planning
* Replication
* Software patching
* Cluster scaling
* Continuous backups and restore to specific timestamp
* Multi AZ setup for DR (disater recovery)
* Scailing capability (vertical and horizontal)


## Amazon Relational Database Service
With Amazon Relational Database Service (Amazon RDS), you can set up, operate, and
scale a relational database in the AWS Cloud. It provides cost-efficient, resizable capacity
for open-standard relational database engines.

**Supported Database Engines**
* Postgres
* Oracle
* MySQL
* MariaDB
* Oracle
* Microsoft SQL Server
* Aurora (AWS Proprietary database)

## RDS Read Replicas for read scalability
You can have up to 5 read replicas that are multi AZ, Cross AZ or Cross Region.

Replicas are ASYNC, so reads are eventually consistent. The replicas can be promoted to their own DB. 

Applications must update the connection string to leverage read replicas. 

## RDS Multi AZ (Disaster Recovery)
By using Amazon RDS, you can run in a Multi-AZ configuration. In a Multi-AZ configuration,
you have a primary and a standby DB instance. Updates to the primary database
replicate synchronously to the standby replica in a different Availability Zone. The primary
benefit of Multi-AZ is realized during certain types of planned maintenance, or in the
unlikely event of a DB instance failure or an Availability Zone failure. Amazon RDS automatically
fails over to the standby so that you can resume your workload as soon as the
standby is promoted to the primary. This means that you can reduce your downtime in the
event of a failure.

**Key points**
* This increases *availability*
* This is for the failover in case of loss of AZ, loss of network, instance or storage failure
* You don't have to manually intervene in apps


## RDS Backups
Amazon RDS has two different ways of backing up data of your database instance: automated
backups and database snapshots (DB snapshots). Backups are automatically enabled in RDS.

#### Automated Backups (Point-in-Time)
With Amazon RDS, automated backups offer a point-in-time recovery of your database.
When enabled, Amazon RDS performs a full daily snapshot of your data that is taken
during your preferred backup window. After the initial backup is taken (each day), then
Amazon RDS captures transaction logs as changes are made to the database.


#### DB Snapshots:
Unlike automated backups, database snapshots with Amazon RDS are user-initiated and
enable you to back up your database instance in a known state at any time. You can also
restore to that specific snapshot at any time.
Similar to the other Amazon RDS features, you can create the snapshots through the
AWS Management Console, with the CreateDBSnapshot API, or with the AWS CLI.
With DB snapshots, the backups are kept until you explicitly delete them; therefore,
before removing any Amazon RDS instance, take a final snapshot before removing it.

## RDS Encryption
For encryption at rest, Amazon RDS uses the AWS Key Management Service (AWS KMS)
for AES-256 encryption. You can use a default master key or specify your own for the
Amazon RDS DB instance. Encryption is one of the few options that must be configured
when the DB instance is created. You cannot modify an Amazon RDS database to enable
encryption. You can, however, create a DB snapshot and then restore to an encrypted DB
instance or cluster.

**Key points**
* Encryption at rest capability with AWS KMS - AES-256 encryption
* SSL certificates ton encrypt data to RDS in flight


## RDS Security
* RDS databases are usually deployed within a private subnet, not in a
public one
* RDS Security works by leveraging security groups (the same concept as
for EC2 instances) – it controls who can communicate with RDS
* IAM policies help control who can manage AWS RDS
* Traditional Username and Password can be used to login to the
database
* IAM users can now be used too (for MySQL / Aurora – NEW!)

## RDS vs Aurora
Amazon Aurora is a MySQL- and PostgreSQL-compatible relational database engine that
combines the speed and availability of high-end commercial databases with the simplicity
and cost-effectiveness of open source databases.
Aurora is part of the managed database service Amazon RDS.

* Aurora is “AWS cloud optimized” and claims 5x performance improvement
over MySQL on RDS, over 3x the performance of Postgres on RDS
* Aurora storage automatically grows in increments of 10GB, up to 64 TB.
* Aurora can have 15 replicas while MySQL has 5, and the replication process
is faster (sub 10 ms replica lag)
* Failover in Aurora is instantaneous. It’s HA native.
* Aurora costs more than RDS (20% more) – but is more efficient

Aurora is a drop-in replacement for MySQL and PostgreSQL relational databases. It is
built for the cloud, and it combines the performance and availability of high-end commercial
databases with the simplicity and cost-effectiveness of open source databases. You can
use the code, tools, and applications that you use today with your existing MySQL and
PostgreSQL databases with Aurora.
The integration of Aurora with Amazon RDS means that time-consuming administration
tasks, such as hardware provisioning, database setup, patching, and backups, are
automated.

When you create an Aurora instance, you create a DB cluster. A DB cluster consists
of one or more DB instances and a cluster volume that manages the data for those instances. An Aurora cluster volume is a virtual database storage volume that spans multiple
Availability Zones, and each Availability Zone has a copy of the DB cluster data.

#### Types of DB instances:
*Primary Instance*  Supports read and write operations and performs all of the data modifications
to the cluster volume. Each Aurora DB cluster has one primary instance.

*Amazon Aurora* Replica Supports read-only operations. Each Aurora DB cluster can
have up to 15 Amazon Aurora Replicas in addition to the primary instance. Multiple
Aurora Replicas distribute the read workload, and if you locate Aurora Replicas in separate
Availability Zones, you can also increase database availability.


## Best Practices for Running Databases on AWS

#### Follow RDS basic operational guidelines
* Monitor your memory, CPU, and storage usage. Amazon CloudWatch can notify you when usage patterns change or when you approach the capacity of your deployment. This helps maintain system performance and availability. 

* Scale up your DB instance when you approach storage capcity limits. Have buffer in storage and memory to accommdate unexpected increases in demand.

* Enable automatic backups, and set the backup window to occur during the daily
low in write IOPS.

* If your client application is caching the Domain Name Service (DNS) data of your
DB instances, set a time-to-live (TTL) value of less than 30 seconds. If the a failover occurs, caching the DNS data for a long time can lead to connection failures if your app tries to connect to an IP address that no longer is in service. 

* Test failover for your DB instance to understand how long the process takes for
your use case and to ensure that the application that accesses your DB instance can
automatically connect to the new DB instance after failover.

#### Allocate sufficient RAM to the DB instance.
An Amazon RDS performance best practice
is to allocate enough RAM so that your working set resides almost completely in memory.

#### Implement Amazon RDS security
Use IAM accounts to control access to Amazon RDS
API actions, especially actions that create, modify, or delete Amazon RDS resources, such
as DB instances, security groups, option groups, or parameter groups, and actions that
perform common administrative actions, such as backing up and restoring DB instances, or
configuring Provisioned IOPS storage.

#### Use right tool to change password
Use the AWS Management Console, the AWS CLI, or the Amazon RDS API to change the password
for your master user. If you use another tool, such as a SQL client, to change the master
user password, it might result in permissions being revoked for the user unintentionally.


#### Use enhanced monitoring to identify OS issues
Amazon RDS provides metrics in real
time for the OS on which your DB instance runs. You can view the metrics for your DB instance by using the console or consume the Enhanced Monitoring JSON output from
CloudWatch Logs in a monitoring system of your choice.

#### Use read replicas
Use read replicas to relieve pressure on your master node with additional
read capacity. You can bring your data closer to applications in different regions and
promote a read replica to a master for faster recovery in the event of a disaster.

## Essentials
**Know what a relational database is.** A relational database consists of one or more tables.
Communication to and from relational databases usually involves simple SQL queries, such
as “Add a new record” or “What is the cost of product x?” These simple queries are often
referred to as online transaction processing (OLTP).

**Know what a nonrelational database is.**  Nonrelational databases do not have a
hard-defined data schema. They can use a variety of models for data management,
such as in-memory key-value stores, graph data models, and document stores. These
databases are optimized for applications that have a large data volume, require low
latency, and have flexible data models. In nonrelational databases, there is no concept
of foreign keys.

**Understand the database options available on AWS.**  You can run all types of databases on
AWS. You should understand that there are managed and unmanaged options available, in
addition to relational, nonrelational, caching, graph, and data warehouses.

**Understand which databases Amazon RDS supports.** Amazon RDS currently supports six
relational database engines:
* Microsoft SQL Server
* MySQL
* Oracle
* PostgreSQL
* MariaDB
* Amazon Aurora

**Understand the operational benefits of using Amazon RDS.**  Amazon RDS is an AWS
managed service. AWS is responsible for patching, antivirus, and the management of the
underlying guest OS for Amazon RDS. Amazon RDS greatly simplifies the process of setting
a secondary slave with replication for failover and setting up read replicas to offload
queries.

**Remember that you cannot access the underlying OS for Amazon RDS DB instances.**  You
cannot use Remote Desktop Protocol (RDP) or SSH to connect to the underlying OS. If
you need to access the OS, install custom software or agents. If you want to use a database
engine that Amazon RDS does not support, consider running your database on an Amazon
EC2 instance instead.

**Understand that Amazon RDS handles Multi-AZ failover for you.** If your primary
Amazon RDS instance becomes unavailable, AWS fails over to your secondary instance
in another Availability Zone automatically. This failover is done by pointing your existing
database endpoint to a new IP address. You do not have to change the connection string
manually; AWS handles the DNS changes automatically.
Remember that Amazon RDS read replicas are used for scaling out and increased
performance. This replication feature makes it easy to scale out your read-intensive
databases. Read replicas are currently supported in Amazon RDS for MySQL, PostgreSQL,
and Amazon Aurora. You can create one or more replicas of a database within a single AWS
Region or across multiple AWS Regions. Amazon RDS uses native replication to propagate
changes made to a source DB instance to any associated read replicas. Amazon RDS also
supports cross-region read replicas to replicate changes asynchronously to another geography
or AWS Region.

