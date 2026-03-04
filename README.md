##Database Migration using AWS DMS##

Project Overview

This project demonstrates how to migrate a MySQL database from a source database to a target database in AWS using AWS Database Migration Service (DMS).

A source RDS database containing company data was migrated to a target RDS database using a DMS replication instance. After the migration task completed, the data was verified by connecting to the database using the MySQL client.

This project demonstrates database migration from on-premise to cloud or cloud-to-cloud using AWS DMS.

AWS Services Used:-

Amazon RDS (MySQL)

AWS Database Migration Service (DMS)

AWS DMS Replication Instance

AWS EC2 / MySQL Client

AWS Security Groups

Architecture:-

Source Database (RDS / On-Premise)
          │
          ▼
AWS DMS Replication Instance
          │
          ▼
Target Database (Amazon RDS MySQL)
          │
          ▼
MySQL Client Verification

Step 1 – Create Source and Target RDS Databases

Two RDS MySQL instances were created:

src-database → Source database

target-database → Target database

Both databases were running in AWS.

Step 2 – Create DMS Replication Instance

A replication instance was created in AWS Database Migration Service.

Example configuration:

Engine version: 3.5.4

Instance type: dms.t3.micro

Status: Available

The replication instance acts as the migration server that moves data from source to target.

Step 3 – Create Source Endpoint

Source endpoint configuration:

Endpoint name: mysql-source

Engine type: MySQL

Server: source RDS endpoint

Port: 3306

This endpoint connects AWS DMS to the source database.


Step 4 – Create Target Endpoint

Target endpoint configuration:

Endpoint name: mysql-target

Engine type: MySQL

Server: target RDS endpoint

Port: 3306

This endpoint connects AWS DMS to the target database.


Step 5 – Create Migration Task

Migration task name:
mysql-migration-task

Migration type:
Full load

This task copies all data from the source database to the target database.

After starting the task, the migration process begins.


Step 6 – Monitor Migration

AWS DMS shows the migration progress.

Full load progress: 100%
Status: Starting / Completed

This indicates the database has been successfully migrated.

Step 7 – Verify Migrated Data

Connected to the target database using MySQL client.

mysql -h <rds-endpoint> -u admin -p

show databases;

companydb
studentdb
mysql
information_schema


Step 8 – Verify Table Data

Use the company database:
use companydb;
show tables;

employees

Check table data:

select * from employees;































