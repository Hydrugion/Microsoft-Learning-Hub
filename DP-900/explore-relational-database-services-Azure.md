# Explore relational database services in Azure

Most Azure database services are fully managed, enterprise-grade performance, built-in high availability, industry-lead innovation.

## Azure SQL service and capabilities

Azure SQL services include:
- SQL Server on Azure Virtual Machines (VMs): a VM running in Azuew with an installation of SQL Server.
- Azure SQL managed instance: A PaaS that provide near 100% compaitibility with on-premises SQL server while abstracting the underlying hardware and operating system. Automaed software update management, backups and other maintenance task.
- Azre SQL database: Fully managed, highly scalable PaaS database service designed for the cloud.
- Azure SQL Edge: SQL engine that optimized for IoT scenarios that need to work with streaming time-serires data

## Comparision Azure SQL services

| |SQL Server on Azure VMs | Azure SQL Managed Instance | Azure SQL Database |
| --- | --- | --- | --- |
| Type of cloud service| 	IaaS |	PaaS |	PaaS
| SQL Server compatibility |	Fully compatible with on-premises physical and virtualized installations. Applications and databases can easily be "lift and shift" migrated without chang. | Near-100% compatibility with SQL Server. Most on-premises databases can be migrated with minimal code changes by using the Azure Database Migration service | Supports most core database-level capabilities of SQL Server. Some features depended on by an on-premises application may not be available.
| Architecture | SQL Server instances are installed in a virtual machine. Each instance can support multiple databases. | Each managed instance can support multiple databases. Additionally, instance pools can be used to share resources efficiently across smaller instances. | You can provision a single database in a dedicated, managed (logical) server; or you can use an elastic pool to share resources across multiple databases and take advantage of on-demand scalability.
| Availability | 99.99% | 99.99% | 99.995%
| Management | You must manage all aspects of the server, including operating system and SQL Server updates, configuration, backups, and other maintenance tasks. | Fully automated updates, backups, and recovery. | Fully automated updates, backups, and recovery.
| Use cases | 	se this option when you need to migrate or extend an on-premises SQL Server solution and retain full control over all aspects of server and database configuration. | Use this option for most cloud migration scenarios, particularly when you need minimal changes to existing applications. | Use this option for new cloud solutions, or to migrate applications that have minimal instance-level dependencies.

## SQl server on Azure VMs

Suitable for migrations and applications requireing acess to oeprating system features that might be unsupported at PaaS level.

## SQL database managed instance

Allow multiple database on the same instance. Have automated backups, software patching, database monitoring.

The managed instances **depend on** other Azure services such as:
- Azure Storage for backups
- Azure Event Hubs for telemetry
- Azure Active Directory for authentication
- Azure Key Vault for transparent data encryption (TDE)
- A couple of other Azure platform service that provide security and supportability features

The managed instances also provide features that is **not available** in Azre SQL database: linked servers, Service Broker, Database Mail.

Use case: lift and shift on-premises SQL server instance and all its databases to the cloud without incurring the management overhead of running SQL server on VMs.

## Azure SQL Database

PaaS, create a managed database server on the cloud and then deploy on this server.

Available as *Single Database* or *Elastic Pool*

**Single database**: quickly setup and run a single database server. Only need to configure, create tables and populate with data. Scale the database by adding more storage, memory, processing power. **Charged per hour per resources**. There is also a *serverless* configuration where Microsoft create its own server and shared among other Azure subscriber (that also use serverless configuration)

**Elastic Pool**: by default multiple database can share the same resources through multiple-tenancy. This model is useful for database which resources vary overtime. Elastic Pool allows using the resources when needed and releasing it when the processing is complete.

Azure database is often used for:
- Modern cloud application that need the latest SQL server feature
- Application that need **high availability**
- System with variable load and need to be scaled up and down quickly

## Azure services for open-sourced databases

Include: MySQL, MariaDB, PostgreSQL. Primary reason is for organizations to quickly migrate from on-premises to Azure cloud without changing too much the application.

**MySQL**: simple to use, open sourced DBMS.

**MariaDB**: newer DBMS by the developer of MySQL. One notable feature is built-in support for temporal data, where a table can hold serveral versions of the data, allowing the application to query data in the past.

**PostgreSQL**: hybrid relational-object database. Can store custom data types, extensible and have the ability to store and manipulate geometric data such as lines, circles and polygons

**Azure database for MySQL**: based on the MySQL community edition. High availability at no additional cost and scalability as required. Have automatic backup with point-in-time restore. Can be deployed in *Single Server* and *Flexible Server*.

**Azure database for MariaDB**: based on the community implementation of MariaDB. Have built in high availability, scaling as needed within seconds, automated backup and point-in-time within 35 days.

**Azure database for PostgreSQL**: provide the same availability, scaling, performance and security as MySQL service. Some feature of on-premises PostgreSQL are not available because concern with extentions that the user can add to the database, such as writing stored procedures in various programing language and interact with the operating system. Can be deployed in *Single Server, Flexible Server* and *Hyper Scale*.

## Summary

- Identify option for Azure SQL services
- Identify option for open-sourced database in Azure