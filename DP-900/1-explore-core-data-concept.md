# Explore core data concepts

## Identify data format

3 types of data:
- Structured: fixed schema ex: Table
- Semi-structures: have some structure but can vary between entities ex: JSON, XML
- Unstructured: ex: Document, Audio, Image, Binary

Data is often stored in 2 type of system:
- File storage
- Databases

## File storage

Factors on determine data format:
- Type of data: Structured, Semi-structured, Unstructured
- Applications and services that will need to read, write and process the data
- The need for the datafile to be readable by human or optimized for efficient storage and processing

File formats:
- Delimited text file: CSV, TSV with secific field delimiter and row terminator. Good choice for **structured data** that need to be accessed by a wide range of applications and services in human-readable format.
- JSON: hierarchical document schema. Good for both structured and semi-structured data.
- XML: use tags enclosed in angle-brackets to define elements and attributes.
- BLOB: store data as raw binary, for **unstructured data**
- Optimized file format:
  - Avro: Row based format. Each record contains a header which describe the data format and data stored as binary. Good for compressing data and minimizing storage and network bandwidth requirements.
  - ORC (Optimized Row Columnar): Column based format. Each file contains *stripes* of data which holds data for a set of columns, index into the rows, data for each row and footer that holds statistical information for each column. Optimizing for read and write operations in Apache Hive.
  - Parquet: Column based format. Each file contains row groups. Data for each columns is stored together in the same row groups. Each rows groups contains chunks of data. Also have a metadata that describe the set of rows in each chunk that helps quickly locate the correct chunk for a given set of rows and retrive the data in the specified columns. Specialized in storing and processing nested data types efficiently and have efficient compression and encoding scheme.
  
## Database

Relational databases:
- Store and query structured data
- Each instances of an entity is assigned a primary key that can be used to reference it. Enable *normalization*.
- Managed and query using Structured Query Language (SQL)

Non-relational databases:
- Key-value databases: Each records consists of a unique key and an associated value.
- Document databases: Specific form of key-value where the value is a JSON document.
- Column famlily databases: Store tabular data. Columns can be divided into groups knows as column-family.
- Graph databases: store entities as nodes and links to model the relationship between them.

## Transactional data processing

- Records *transactions* that model an event which need to be tracked. Think transaction as a small, discrete, unit of work.
- Work performed by transactional systems often referred to as Online Transactional Processing (OLTP)

OLTP:
- Rely on database system which datastore is optimized for both read and write to support CURD workload (create, update, retrieve, delete)
- Operation have to be applied transactionally to ensure data integrity.
- Enfore transactions that support ACID schematics:
  - Atomicity
  - Consistency
  - Isolation
  - Durability
  
## Analytical data processing

- Typically use read-only (or read-mostly) systems that store vast volumns of historical data or business metrics.
- Common architecture for enterprise-scale analytics:
 - Data files stored in a central data lake
 - ETL process copies data from files and OLTP databases into data warehouse that optimized for read. Data warehouse schema is based on *fact* tables that contains numeric values you want to analyze and related *dimension* table that represent the entities you want to measure.
 - Data in warehouse can be aggregated and loaded into an online analytical processing (OLAP) model or *cube*. Numeric values (measures) from fact tables are calculated for intersection of dimension tables.
 - Data in data lake, warehouse and analytical model can be queried to produce reports, visualization and dashboards.
 
*Data lakes* are where large volumn of file-based data are collected and analyzed.

*Data warehouse* are established ways to store data in relational schema that optimized for read-operation.

*OLAP model* is an aggregated type of data storage that optimized for analytical workload. Data aggregations are across dimensions at different levels, enable *drill up/down* to view aggregation at multiple hierarchial levels.

Type of user across the stages of architecture:
- Data scientists: work directly with data files in datalake to explore and model data
- Data analysts: query tables directly in data warehouse to produce reports and visualizaions
- Business users consume pre-aggregated data in analytical model in the form of reports or dashboards

## Summary

- Identify common data formats
- Describe options for storing data in files
- Describe options for storing data in databases
- Describe characteristics of transactional data processing solutions
- Describe characteristic of analytical data processing solutions
