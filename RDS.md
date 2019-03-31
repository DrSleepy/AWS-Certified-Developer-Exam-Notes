# RDS - Relation Database Service

RDS is an SQL database such as MySQL, Oracle, MariaDB etc. Amazon's own RDS is Amazon Aurora.

## RDS - Backups

There are 2 types of backups for AWS:

**Key note: A restored backup of either type will result in a new RDS instance, resulting in a new DNS endpoint**

1. Automated Backups -
   1. Allows you to recover your database at any point within a retention period
   2. A retention period can be between 1 to 35 days
   3. Automate Backups will take a fully daily snapshot of the database
   4. Along with the snapshot, tt will also store transation logs throughout the day
   5. Recovering an automated backup will choose the most recent daily back up before applying transation logs relevant to that day. This allows you to do a point in time recovery down to a second, within the retention period
   6. Automated backups are enabled by default
   7. The backups are stored in S3, giving you free storage space equal to the size of your database
   8. Backups are taken within a defined window. During this time, you may experience higher latency
   9. The backup is deleted once you delete the RDS instance, unlike database snapshots
2. Databse Snapshots -
   1. Snapshots are done manually
   2. They are stored even after you delete the original RDS instance, unlike automated backups

## RDS - Encryption

1. Database Encryption is done using AWS KMS (Key Management Service).
2. Once a database has been encrypted, the same will be done to all its replicas.
3. As it stands, encrypting an exisiting DB instance is not supported.
   1. To encrypt a DB instance: Create snapshot of DB > Make copy of snapshot > encrypt copy

Encryption supported for the follow databases:

1. MySQL
2. Oracle
3. SQL Server
4. PostgreSQL
5. MariaDB
6. Aurora

## RDS - Multi-AZ

Multi-AZ is for disater recovery ONLY.
It is not used for improving performance. Read Replicas are used for improving performance.

Multi-AZ allows you to have an exist copy of your database in another Availability Zone.
AWS handles replicating your DB into other Availability Zones whilst still keeping in sync with the primary DB.

You NEVER work with IP addresses when establishing a conneciton with an RDS but rather through a DNS.
This is because if the database is phyisically destroyed, it allows amazons to re-route the url of the database to its healthy replica.

Supported Muli-AZ Databases:

1. MySQL
2. Oracle
3. SQL Server
4. PostgreSQL
5. MariaDB
6. Aurora (on by default)

## RDS - Read Replica

Read Replica is used for scaling, NOT for disater recovery.
For disaster recovery, use Multi-AZ.

Read Replicas allows you to have a read-only copy of your database.
This is achieved by asynchronous replication from the primary RDS instance to the read replica.
Replicas are used for very heavy read-heavy database workloads.

1. Must have automatic backups turned on in order to deploy a read replica
2. You can have up to 5 read replica copies of any database
3. You can have read replicas of read replicas (will increase latency)
4. Each read replica will have its own DNS (URL) endpoint
5. A read replica can have Multi-AZ
6. Read replicas can be changed to become their own databases.
   1. This will break the replication
7. Read replica can be hosted in an entirely different region

Supported Read Replica Databases:

5. MySQL
6. PostgreSQL
7. MariaDB
8. Aurora
