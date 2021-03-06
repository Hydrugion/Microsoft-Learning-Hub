# Explore data roles and services

## Job roles in world of data

Three key jobs:
- **Database administrators**: manage databases, permissions to users, storing backup copies of data, restore data in the event of failure
- **Data engineers**: manage infrastructure and processes for data integration across the organization, apply data cleaning routines, identifying data goverment rules and implementing pipelines to transfer and transform data between system
- **Data analysts**: explore and analyze data to create visualizations and charts that enable organization to make informed decision

Database administrator:
- Responsible for design, implementation, maintenance and operational aspect of on-premises and cloud-based database systems
- Responsible for overall availability and consistent performance and optimization of databases
- Implement policies, tools, processes for backup and recovery in case of disaster (natural or human-made)
- Manage security of the data, grant privileges to data users

Data engineer:
- Collaborate with stakeholders to design and implement data-related workloads (ingestion pipelines, cleasing, transformation) and data stores for analytical workloads.
- Use wide range of data technologies include relational and non-relational databases, file stores, data streams.
- Responsible for ensuring data privacy within the cloud and spanning from in-premises to cloud data stores.
- Own the management and monitoring of data pipelines to ensure performace

Data analyst:
- Maximize the value of data assets by exploring data, identify trends and relationships
- Design and build analytical models
- Enable advanced analytics capabilities through reports and visualization
- Process raw data into relevant insights based on business requirement

## Data services

**Microsoft Azure** is a cloud platform, includes many services to support cloud solutions including transactional and analytical data workloads.

### Azure SQL

A collective name for a family of relational databases solutions based on Microsoft SQL Server database engine.
- Azure SQL Database: a fully managed platform-as-a-service (PaaS) database hosted in Azure
- Azure SQL Managed Instance: a hosted instance of SQL Server with automated maintenance that allow more flexible configuration than above but with more administrative responsibility for the owner
- Azure SQL VM: a virtual machine with an installation of SQL Server for maximum configurability and full management responsibility

Database administrators provision and manage Azure SQL database systems to support line of business applications that need to store transactional data

Data engineer use Azure SQL database systems as sources for data pipelines that perform ETL operations to ingest the transactional data into analytical solutions.

Data analyst query Azure SQL database directly to create reports and visualizations.

### Azure Database for open-source relational databases

Azure includes managed services for popular open-sourced relational database systems
- MySQL
- MariaDB
- PostgreSQL

### Azure CosmosDB

Azure CosmosDB is a global-scale non-relational database system, enable store and manage data as JSON, key-value pairs, column-families and graphs.

### Azure storage

Azure storage is a core Azure service that enables data storing in:
- Blob containers: scalable, cost-effective storage for binary files.
- File shares: network file shares
- Tables: key-value storage for applications that need to read and write data value quickly

Data engineer use Azure Storage to host data lakes - blob storage with a hierarchical namespace that enables files to be organized in folders in a distributed file system

Questions: similariry to HDFS or Redis?

### Azure Data Factory

Azure data factory is a service that enables defining and scheduling of data pipelines to transfer and transform data, can be integrated with other Azure services.

Data engineer use it to build ETL solutions that populates analytical data stores with data from transactional systems across organization

### Azure Synapse Analytics

Azure Synapse Analytics is a comprehensive, unified data analytics solution that provides a single interface for multiple analytical capabilities:
- Pipelines: based on the same technology as Azure Data Factory
- SQL: highly scalable SQL database engine, optimized for data warehouse workloads
- Apache Spark: open-sourced distributed data processing engine
- Azure Synapse Data Explore: high performance data analytics solution that is optimized for real-time querying of log and telementry data using Kusto Query Language (KQL)

Data engineer can use Azure Synapse Analytics to create unified data analytics solution that combines data ingestion piplines, data warehouse storages and data lakes into single service.

Data analysts can use SQL and Spark pools through interactive notebooks to explore and analyze data, integrate with services such as Azure Machine Learning and Microsoft PowerBI to create data models and extracts insights from data.

### Azure Databricks

Azure Databricks is an Azure-integrated version of the popular Databricks platform which combines Spark with SQL database semantics and integrated management interface to enable large-scale data analytics

Data engineer can use it to create analytical data stores.

Data analysts can use the native notebook support to query and visual data in web-based interface

### Azure HD Insight

Azure HD Insight is an Azure service that provides Azure-hosted clusters for popular Apache open-sourced big data processing technologies:
- Apache Spark: distributed data processing engine
- Apache Hadoop: distributed system that use MapReduce jobs to process large volumes of data efficiently across multiple cluster nodes
- Apache HBase: large-scale NoSQL data storage and querying
- Apache Kafka: message broker for data streaming processing
- Apache Storm: real-time data processing through a topology of spouts and bolts

Data engineer can use it to support big data analytics workloads that depends on multiple Apache technologies.

### Azure Stream Analytics

Azure Stream Analytics if a real-time stream processing engine that capture streams of data then perform ETL operations.

### Azure Data Explorer

Azure Data Explorer is a standalone service that provides the same high-performance querying of log and telemetry data as Azure Synapse Data.

### Azure Purview

Azure Purview provides a solution for enterprise-wide data governance and discoverability by creating a map of data and tracking data lineage across multiple data sources and systems.

### Microsoft PowerBI

Microsoft PowerBI is a platform for analytical data modeling and reporting that analysts can use to create and share interactive data visualizations. Reports can be created using the desktop version, published and delivered through web-based reports and apps.

## Summary

- Identify common data professional roles
- identify common cloud services
