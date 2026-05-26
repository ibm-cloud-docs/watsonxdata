---

copyright:
  years: 2022, 2026
lastupdated: "2026-04-30"

keywords: lakehouse, remote data, cloudera, {{site.data.keyword.lakehouse_short}}

subcollection: watsonxdata

---

{:javascript: #javascript .ph data-hd-programlang='javascript'}
{:java: #java .ph data-hd-programlang='java'}
{:ruby: #ruby .ph data-hd-programlang='ruby'}
{:php: #php .ph data-hd-programlang='php'}
{:python: #python .ph data-hd-programlang='python'}
{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:video: .video}

# Querying Cloudera tables using Presto engine
{: #data_stream_cloudera_presto_query}

## About this task
{: #data_stream_cloudera_presto_query1}

After setting up the Cloudera integration, you can query Hive tables stored in Cloudera HDFS from {{site.data.keyword.lakehouse_full}} using the Presto engine. This guide covers query operations and examples.

For information about setting up the integration, see [Setting up Cloudera integration with Presto engine](/docs/watsonxdata?topic=watsonxdata-data_stream_cloudera_presto_setup).

## Before you begin
{: #data_stream_cloudera_presto_query2}

Ensure that you have completed the setup process:

- HDFS storage component is configured in {{site.data.keyword.lakehouse_short}}
- Catalog is created and associated with Presto engine
- Tables are created in Cloudera Hue editor

## Procedure
{: #data_stream_cloudera_presto_query3}

After creating tables in Cloudera, they will be automatically available in {{site.data.keyword.lakehouse_short}} once the catalog is configured.

1. Navigate to **Query Workspace** in {{site.data.keyword.lakehouse_short}}.
2. Select your configured catalog.
3. Expand the schema to see available tables.
4. Query all schemas from the catalog:

   ```sql
   SHOW SCHEMAS FROM <catalog_name>;
   ```
   {: codeblock}

   Example output:

   ```sql
   Schema
   --------------------------
   default
   employee_db
   sales_db
   information_schema
   ```
   {: screen}

5. Query tables in a specific schema:

   ```sql
   SHOW TABLES FROM <catalog_name>.<schema_name>;
   ```
   {: codeblock}

   Example output:

   ```sql
   Table
   -----------------
   employee
   department
   salary_history
   ```
   {: screen}

6. View the structure of a table:

   ```sql
   DESCRIBE <catalog_name>.<schema_name>.<table_name>;
   ```
   {: codeblock}

   Example output:

   ```sql
   Column       | Type                  | Extra | Comment
   -------------|-----------------------|-------|--------
   id           | integer               |       |
   name         | varchar               |       |
   department   | varchar               |       |
   salary       | decimal(10,2)         |       |
   ```
   {: screen}

7. Query data from Hive tables:

   ```sql
   SELECT * FROM <catalog_name>.<schema_name>.<table_name> LIMIT 10;
   ```
   {: codeblock}

   Example output:

   ```sql
   +---------------+--------------+------------+-----------------+
   | id            | name         | department | salary          |
   +---------------+--------------+------------+-----------------+
   | 1             | John Doe     | IT         | 75000.00        |
   | 2             | Jane Smith   | HR         | 65000.00        |
   | 3             | Bob Johnson  | Finance    | 80000.00        |
   +---------------+--------------+------------+-----------------+
   ```
   {: screen}

8. Count rows in a table:

   ```sql
   SELECT COUNT(*) FROM <catalog_name>.<schema_name>.<table_name>;
   ```
   {: codeblock}

9. Perform complex queries with filtering and aggregation:

   ```sql
   SELECT
       department,
       COUNT(*) as employee_count,
       AVG(salary) as avg_salary
   FROM <catalog_name>.<schema_name>.<table_name>
   WHERE salary > 60000
   GROUP BY department
   ORDER BY avg_salary DESC;
   ```
   {: codeblock}

## Results
{: #data_stream_cloudera_presto_query4}

You can now query Hive tables from Cloudera HDFS using Presto. The queries execute directly on the data in HDFS without copying data into {{site.data.keyword.lakehouse_short}}.

## Related information
{: #data_stream_cloudera_presto_query5}

- [Integrating Cloudera in {{site.data.keyword.lakehouse_short}}](/docs/watsonxdata?topic=watsonxdata-data_stream_cloudera1)
- [Setting up Cloudera integration with Presto engine](/docs/watsonxdata?topic=watsonxdata-data_stream_cloudera_presto_setup)
- [Cloudera Data Platform documentation](https://docs.cloudera.com/)
- [Apache Hive documentation](https://hive.apache.org/)
- [Apache HDFS documentation](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsUserGuide.html)
