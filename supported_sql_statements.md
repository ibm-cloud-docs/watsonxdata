---

copyright:
  years: 2022, 2024
lastupdated: "2024-02-28"

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

# Supported SQL statements
{: #supported_sql_statements}

Presto queries are case-sensitive. For more information see [Presto case-sensitive behavior](watsonxdata?topic=watsonxdata-presto_behavior){: external}.

The following SQL statements are supported in {{site.data.keyword.lakehouse_full}} through different connectors.
{: shortdesc}

| Connector | `CREATE SCHEMA` | `CREATE TABLE` | `INSERT INTO` | `SELECT` | `SELECT` (Complex) | `ALTER TABLE` | `ALTER SCHEMA` | `DELETE` | `GRANT` | `REVOKE` | `SHOW GRANTS` | `SHOW ROLES` | `SHOW ROLE GRANTS` | `UPDATE` | `DROP TABLE` | `CREATE ROLE` | `CREATE VIEW` | `DROP SCHEMA` | `DROP VIEW` |
| :-------------- | :-------------: | :-------------:| :-------------:| :-------------:| :-------------: | :-------------: | :-------------: | :-------------: | :-------------: | :-------------:| :-------------:| :-------------: | :-------------: | :-------------: | :-------------: | :-------------: | :-------------: | :-------------: | :-------------: |
|**Iceberg**| ✓    | ✓   | ✓  | ✓  | ✓  | ✓  | `X`   | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | ✓  | `X`  | ✓  | ✓  | ✓  |
|**MySQL**| `X`    | ✓  | ✓  | ✓  | ✓  | `X`  | `X`   | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | ✓   | `X`  | `X`  | `X`  | `X`  |
|**PostgreSQL**| `X`    | ✓   | ✓  | ✓  | ✓  | ✓  | `X`   | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | `X`  |
|**MongoDB**| `X`    | ✓   | ✓  | ✓  | ✓  | ✓  | `X`   | `✓`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | `X`  |
|**Hive**| ✓    | ✓   | ✓  | ✓  | ✓  | `X`  | `X`   | ✓  | ✓  | ✓  | `X`    | ✓  | ✓  | `X`  | ✓  | ✓  | ✓  | ✓  | ✓  |
|**Kafka**| `X`    | `X`   | `X`  | ✓  | ✓  | `X`  | `X`   | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
| **Memory**| ✓    | ✓   | ✓  | ✓  | ✓  | `X`  | `X`   | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | ✓  | `X`  | ✓  | ✓  | ✓  |
|**TPCH**| `X`    | `X`   | `X`  | ✓  | ✓  | `X`  | `X`   | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
|**TPCDS**| `X`    | `X`   | `X`  | ✓  | ✓  | `X`  | `X`   | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
| **System**| `X`    | `X`   | `X`  | ✓  | ✓  | `X`  | `X`   | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
| **JMX**| `X`    | `X`   | `X`  | ✓  | ✓  | `X`  | `X`   | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
|**Db2**| ✓    | ✓   | ✓  | ✓  |  -- | ✓  | `X`   | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | ✓  | `X`  | ✓  | ✓  | `X`  |
|**{{site.data.keyword.netezza_short}}**| ✓    | ✓   | ✓  | ✓  |  -- | ✓  | `X`   | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | ✓  | `X`  | ✓  | ✓  | X  |
|**SingleStore**| `X`    | ✓   | ✓  | ✓  | ✓  | ✓  | `X`   | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | `X`  |
|**Elasticsearch**| `X`    | `X`   | `X`  | ✓  | ✓  | `X`  | `X`   | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
|**Teradata**| `X`    | ✓   | ✓  | ✓  | ✓   | ✓  | `X`   | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | `X`  |
|**Snowflake**| `X`    | ✓   | ✓  | ✓  | ✓   | ✓  | `X`   | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | `X`  |
|**IBM Data Virtualization Manager for z/OS**| `X`    | `X`   | `X`  | ✓  | `X`   | `X`  | `X`   | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
{: caption="Table 1. SQL statements and supporting connectors" caption-side="bottom"}

## Limitations
{: #connector_limitations}

1. For `CREATE TABLE`, **MySQL** connector supports only `CREATE TABLE AS`.
2. For `CREATE TABLE`, **Snowflake** connector also supports `CREATE TABLE AS`.
3. For `ALTER TABLE`, **MongoDB** connector supports only `TABLE RENAME`.
4. For `DELETE`, **MongoDB** connector supports only `WHERE` clause. It supports `OR` condition queries with the same columns as operands.
5. For `ALTER TABLE`, **Teradata** connector supports only `ADD COLUMN` and `DROP COLUMN`. `DROP COLUMN` does not drop the first column.
6. **Db2** connector partially supports `ALTER TABLE`, `CREATE VIEW`, and `DROP SCHEMA`.
7. **{{site.data.keyword.netezza_short}}** connector partially supports `ALTER TABLE` and `CREATE VIEW`.
8. **MySQL**, **PostgreSQL**, **MongoDB**, **Db2**, **Teradata**, **Snowflake**, **SQL Server**, and **{{site.data.keyword.netezza_short}}** connectors support `DROP TABLE` only when enabled in catalog.
9. The `CREATE SCHEMA`, `CREATE TABLE`, `DROP SCHEMA`, `DROP TABLE`, `DELETE`, `DROP VIEW`, `ALTER TABLE`, and `ALTER SCHEMA` are not available for database-based catalogs in the **Data Manager** UI.
10. For **Db2**, you can create the view for a table only if that table is in the same catalog and the same schema.
11. For **{{site.data.keyword.netezza_short}}**, you can create the view for a table only if that table is in the same catalog and the same schema.

 For `CREATE TABLE`, Iceberg connector supports `sorted_by` table property. When you create the table, specify an array of one or more columns that are involved in sorting. To disable the feature, set the session property `sorted_writing_enabled` to false.
 {: note}

For more information on supported data types, see [Supported data types](watsonxdata?topic=watsonxdata-supported_datatypes){: external}.
