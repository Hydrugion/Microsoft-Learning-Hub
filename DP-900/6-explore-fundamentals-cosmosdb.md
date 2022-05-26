# Explore fundamentals of CosmosDB

**Azure CosmosDB** is a highly scalable cloud database service for NoSQL data.

## Describe Azure CosmosDB

**Azure CosmosDB** supports multiple APIs that enable developers to use common programing sematics of many kinds of data store. The internal data structure is abstracted, enable the developers to use CosmosDB to store and query data with familiar APIs.

![cosmosdb](img/azure-cosmos-db.png)

Cosmos DB uses indexes and partitioning to provides fast read and write performance and scale to massive volume of data. Multi-region writes can be enabled so that globally distributed users can work on their own data replica.

Cosmos DB is highly suitable for:
- IoT and telematics: ingest large amounts of data in frequent burst of activity.
- Retail and marketing: storing catalog data and vent sourcing in order processing pipelines
- Gaming: low latency for engaging experience
- Web and mobile application

## Identify Azure Cosmos DB APIs

When provision a new Cosmos DB, the API used have to be selected and cannot be changed after creation.

**Core (SQL) API**: the native API in Cosmos DB manages data in JSON format and despite being a NoSQL data storage, SQL syntax can be used to work with data.

**MongoDB API**: one of the popular open sourced database. Enable developers to use MongoDB client libraries to code and work with data in Azure Cosmos DB

**Table API**: work with data in key-value tables similar to Azure Table Storage. Cosmos DB offer greater scalability and performance compare to Azure Table. 

**Cassandra API**: compatible with the open sourced Apache Cassandra, a column-family storage structure. Cassandra support syntax based on SQL.

**Gremlin API**: used with data in graph structure, which entities are defined as verticies and relationship as edges. Gremlin syntax includes functions to operate on vertices and edges.

## Summary

- Describe key features and capabilities of Cosmos DB
- Identify the APIs supported in Azure Cosmos DB
- Provision and use an Azure Cosmos DB instance