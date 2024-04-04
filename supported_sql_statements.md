---

copyright:
  years: 2022, 2024
lastupdated: "2024-04-03"

keywords: lakehouse, SQL statements, connectors, watsonx.data

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

# SQL statements supported in {{site.data.keyword.lakehouse_full}} for Presto
{: #supported_sql_statements}

Presto queries are case-sensitive. For more information see [Presto case-sensitive behavior](watsonxdata?topic=watsonxdata-presto_behavior){: external}.

The following SQL statements are supported in {{site.data.keyword.lakehouse_full}} for Presto through different connectors.
{: shortdesc}

| Statements | `Iceberg` | `MySQL` | `PostgreSQL` | `MongoDB` | `Hive` | `Kafka` | `TPCH` | `TPCDS` | `System` | `JMX` | `Db2` | `IBM Netezza` | `Memory` | `Iceberg in AWS Glue` | `AWS Glue as Meta Store` | `Hudi` | `SQL Server` | `SingleStore` | `Elasticsearch` | `Teradata` | `Snowflake` | `SAP HANA` | `Delta` | `IBM Data Virtualization Manager for z/OS` |
| :-------------- | :-------------: | :-------------:| :-------------:| :-------------:| :-------------: | :-------------: | :-------------: | :-------------: | :-------------: | :-------------:| :-------------:| :-------------: | :-------------: | :-------------: | :-------------: | :-------------: | :-------------: | :-------------: | :-------------: | :-------------: | :-------------: | :-------------: | :-------------: | :-----------------------: |
|ALTER TABLE| ✔    | ✔   | ✔  | ✔  | ✗  | ✗  | ✗  | ✗  | ✗  | ✗  | ✔  | ✔  | ✗  | ✗  | ✗  | ✗  | ✔  | ✔  | ✗  | ✔  | ✔  | ✗  | ✗  | ✗  |
|ALTER VIEW RENAME TO| ✔    | ✗   | ✗  | ✗  | ✗  | ✗  | ✗  | ✗  | ✗  | ✗  | ✗  | ✗  | ✗  | ✗  | ✗  | ✗  | ✗  | ✗  | ✗  | ✗  | ✗  | ✗  | ✗  | ✗  |
|ANALYZE|	✗ |	✗ |	✗ |	✗ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|CREATE ROLE|	✗ |	✗ |	✗ |	✗ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|CREATE SCHEMA|	✔ |	✗ |	✗ |	✗ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✔ |	✔ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|CREATE TABLE|	✔ |	✔ |	✔ |	✗ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✔ |	✔ |	✔ |	✗ |	✔ |	✗ |	✔ |	✔ |	✗ |	✔ |	✔ |	✔ |	✔ |	✗ |
|CREATE TABLE AS|	✔ |	✔ |	✔ |	✔ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✔ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|CREATE VIEW|	✔ |	✗ |	✗ |	✗ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|DEALLOCATE PREPARE|	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|DESCRIBE|	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|DESCRIBE INPUT|	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|DESCRIBE OUTPUT|	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|DROP ROLE|	✗ |	✗ |	✗ |	✗ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|DROP SCHEMA|	✔ |	✗ |	✗ |	✗ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|DROP TABLE|	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✗ |	✗ |	✔ |	✔ |	✔ |	✔ |	✔ |	✗ |	✗ |	✗ |	✔ |	✔ |	✗ |	✔ |	✔ |	✔ |	✔ |	✗ |
|DROP VIEW|	✔ |	✗ |	✗ |	✗ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|EXECUTE|	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|EXPLAIN|	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|EXPLAIN ANALYZE|	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|GRANT|	✗ |	✗ |	✗ |	✗ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|GRANT ROLES|	✗ |	✗ |	✗ |	✗ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|INSERT|	✔ |	✔ |	✔ |	✔ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✔ |	✔ |	✔ |	✗ |	✔ |	✗ |	✔ |	✔ |	✗ |	✔ |	✗ |	✗ |	✗ |	✗ |
|PREPARE STATEMENT|	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|RESET SESSION|	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|REVOKE|	✗ |	✗ |	✗ |	✗ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|REVOKE ROLES |	✗ |	✗ |	✗ |	✗ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|SELECT|	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✗ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |
|SELECT(Complex)|	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✗ |	✗ |	✔ |	✔ |	✗ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✗ |
|SELECT ROLE|	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|SET SESSION|	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|SHOW CATALOGS|	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|SHOW COLUMNS|	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|SHOW CREATE TABLE|	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|SHOW CREATE VIEW|	✔ |	✗ |	✗ |	✗ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|SHOW FUNCTIONS|	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|SHOW GRANTS|	✔ |	✗ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✗ |	✗ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✗ |	✗ |
|SHOW ROLE GRANTS|	✗ |	✗ |	✗ |	✗ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|SHOW ROLE|	✗ |	✗ |	✗ |	✗ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|SHOW SCHEMAS|	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|SHOW SESSION|	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|SHOW STATS|	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|SHOW TABLES|	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|TRUNCATE|	✗ |	✔ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✔ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|USE statement|	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
|VALUES|	✔ |	✔ |	✔ |	✔ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✔ |	✔ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |	✗ |
{: caption="Table 1. SQL statements and supporting connectors" caption-side="bottom"}

## Features
{: #connector_features}

1. For **Iceberg** connector:
- You can delete data from tables by using `DELETE FROM` statement for **Iceberg** connector.
- You can specify the table property delete_mode for new tables by using either copy-on-write mode or merge-on-read mode (default).
2. For `DELETE FROM` statement for **Iceberg** connector:
- Filtered columns only support comparison operators, such as EQUALS, LESS THAN, or LESS THAN EQUALS.
- Deletes must only occur on the latest snapshot.
- For V1 tables, the **Iceberg** connector can only delete data in one or more entire partitions. Columns in the filter must all be identity-transformed partition columns of the target table.
3. For `CREATE TABLE`, **Iceberg** connector supports `sorted_by` table property.
- When you create the table, specify an array of one or more columns that are involved.

## Limitations
{: #connector_limitations}

1. **MySQL** connector supports only `CREATE TABLE AS` for `CREATE TABLE` statement.
2. **Snowflake** connector also supports `CREATE TABLE AS` for `CREATE TABLE` statement.
3. **MongoDB** connector supports only `TABLE RENAME` for `ALTER TABLE` statement.
4. **MongoDB** connector does not support complex `DELETE` involving `OR` statements with different columns for `DELETE` statement.
5. **Teradata** connector supports only `ADD COLUMN` and `DROP COLUMN` for `ALTER TABLE` statement. `DROP COLUMN` does not drop the first column.
6. **Db2** connector partially supports `ALTER TABLE`, `CREATE VIEW`, and `DROP SCHEMA` statements.
7. **{{site.data.keyword.netezza_short}}** connector partially supports `ALTER TABLE` and `CREATE VIEW` statements.
8. **MySQL**, **PostgreSQL**, **MongoDB**, **Db2**, **Teradata**, **Snowflake**, **SQL Server**, and **{{site.data.keyword.netezza_short}}** connectors support `DROP TABLE` statement only when enabled in the catalog.
9. For database-based catalogs the `CREATE SCHEMA`, `CREATE TABLE`, `DROP SCHEMA`, `DROP TABLE`, `DELETE`, `DROP VIEW`, `ALTER TABLE`, and `ALTER SCHEMA` statements are not available in the **Data Manager** UI.
10. For **Db2** and **{{site.data.keyword.netezza_short}}** connectors, you can create the view for a table only if that table is in the same catalog and the same schema.
11. For **Iceberg**, **Db2**, **{{site.data.keyword.netezza_short}}**, **Memory** and **Hive** connectors, `DROP SCHEMA` can do `RESTRICT` by default.

For more information on supported data types, see [Supported data types](watsonxdata?topic=watsonxdata-supported_datatypes){: external}.
