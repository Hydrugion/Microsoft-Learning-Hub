# Work with data in Azure Databricks

In Azure Databricks, Data scientists use Dataframes to structure their data. A Dataframe is equivalent to a relational table in SparkSQL.

## Understand dataframe

Spark use 3 different APIs based on the Resilience Distributed Dataset (RDD):
- RDDs
- Dataframes
- Datasets

Dataframe are the distributed collection of data, organized into rows and columns. Each columns have an associated name and type

    # load using SQL
    df = spark.sql("SELECT * FROM nyc_taxi_csv")

    # load from DBFS
    df = spark.read.csv("dbfs:/FileStore/tables/nyc_taxi.csv", header=True, inferSchema = true)

    # Size
    df.size()

    # Structure
    df.printSchema()

    # Show contents
    df.show()

## Query dataframe

read,write
select, take, sort, filter
union, join, groupby
summary

## Visualize data

`display` and `displayHTML` function

Data can be displayed as bar, pie, histogram, maps, images,...

Plot options:
- Choose columns to be used as axes
- Choose to group series of data
- Choose aggregations to be used with the grouped data

## Summary

- Describe dataframes
- Query dataframes
- Visualize data
