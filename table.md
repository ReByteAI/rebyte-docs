## What is a Table?

> Handle structured data for your assistant.

Table is a virtual database that represents a read-only view to your original data source. The original data source can be a csv, Excel, postgres, mysql, parquet, JSON, sqlite, snowflake, s3, bigquery etc.

**Table** has the following characteristics:
* **Read-only**: Table is a read-only view to your original data source, which means rebyte never writes to your original data source.
* **Partial View**: you can select a subset of columns and rows from your original data source to create a table. For example, you can hide sensitive columns, or filter out rows that are not relevant to your assistant. **This means you never need to alter your original data source**.
* **Transient**: Table is transient, which means it's not persisted in rebyte's database, it's only available during the execution of the tool. This is to ensure that your data is secure and private.


![img](https://res.cloudinary.com/dfjwtidnh/image/upload/v1721433515/table_kwozfl.png)


## Tableset
Tableset is a collection of tables, tableset is the unit of access control, which means tables in the same tableset share the same access control in terms of who can access the table.

## Table Lifecycle

### Build Time
Two things need to be specified when building a table:

* **Define Data Source**: the original data source, such as a csv file, a database table, etc.
* **Define Table View**: how to map the original data source to the table, such as selecting columns, filtering rows, etc.

### Query Time
You can build a **tool** to enable a natural language query to table. Here are three steps:
* **Load table action**: Load the table data into memory, and output a complete table schema. 
* **SQL Generation By LLM**: combine the table schema with the natural language query to generate an SQL query. You can use any LLM. In the future, we will provide a specialized model for just outputting SQL queries. 
* **Query table action**: search the table with the generated SQL query, and output the result.
   
## Refer To the Original Data Source
When creating a table, you need to provide an SQL query to specify which part of the original data source you want to use to build the table. 

The most common use case is just to include all columns and rows from the original data source, in this case, The SQL query is just 
```sql
SELECT * FROM src
```
ReByte always uses 'src' as the alias of the original data source.
* for file-based data source, for example, csv, excel, parquet, the 'src' refers to the whole data in the file.
* for database-based data source, for example, postgres, mysql, the 'src' refers to the whole database, use 'src'.'table_name' to refer to a specific table in your remote database.
   
## Data Source
* Csv
* Excel
* Postgres
* Parquet
* JSON
* SQLite

## Table Actions

In ReByte Tool Builder, there are two actions related to table:
* **Load Table**: Load the table data into memory, and output a complete table schema, schema includes column names, column types, possible values, nullable, primary key, unique value count, etc. With the help of complete table schema, Almost **ALL** LLM can generate precise SQL query over the table.
* **Query Table**: run an SQL query over the table, and output the result, usually the SQL is generated by LLM action.

## Important Notes
* **Data Security**: Table is transient, which means it's not persisted in rebyte's database, it's only available during the execution of the tool. But tool run logs may contain the table data, tool run logs are stored in rebyte's database, so be careful when using sensitive data in the table. 
* **Table Size**: Currently we don't have a limit on the table size, from our experience, a table with 1M rows and 10 columns can be processed in a few seconds.
* **Maximum Rows Per Query**: Only the first 1024 rows are returned in the query table action, this is to prevent the assistant from returning too much data. If you see error, try to use a more specific query, or set a LIMIT in the SQL query. 