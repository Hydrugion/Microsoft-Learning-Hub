# Exlore fundamental relational data concept

Relational database model was designed to solve the problem of arbitrary data structures. 

## Understand relational data

**Tables**: model of real world entities
- Contains rows that represents an instance of that entity
- Structured, each row have the same number of column
- Each column have a specific data type

## Understand normalization

**Normalization**: a schema design process that minimize data dupication and enforce data integrity

Some rules for normalization:
1. Separate each entitiy into its own table
2. Separate each discrete attribute into its own columns
3. Uniquely identify each entity instance using a primary key
4. Use foreign key columns to link related entities

## SQL

Structured query language: standard language for relational database management system.

**SQL statement types**: 3 main logical group
- Data definition language (DDL)
- Data control language (DCL)
- Data manipulation language (DML)

DDL statements: create, modify, remove tables and other objects in database (table, stored procedures, views, ...)
- CREATE: create new object in the database
- ALTER: modify the structrure of an object
- DROP: remove an object
- RENAME: rename an existing object

DCL statements: manage acess to objects in database by granting, denying, revoking permissions to specific users or groups
- GRANT
- DENY
- REVOKE

DML statements: manipulate rows in tables.
- SELECT
- INSERT
- UPDATE
- DELETE

## Describe database object

Some database objects: view, stored procedure and index
- **View**: virtal table as a result of a SELECT query.
- **Stored procedures**: a SQL statement that can be run on command
- **Index**: A structure that enables the queries to locate rows in a table quicker

## Summary

- Identify characteristics of relational data
- Define normalization
- Identify types of SQL statement
- Identify common relational database object
