---

copyright:
  years: 2022, 2023
lastupdated: "2023-09-27"

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

Following SQL statements are supported in {{site.data.keyword.lakehouse_full}} through different connectors.
{: shortdesc}

| Connector | `CREATE SCHEMA` | `CREATE TABLE` | `INSERT INTO` | `SELECT` | `SELECT` (Complex) | `ALTER TABLE` | `ALTER SCHEMA` | `DELETE` | `GRANT` | `REVOKE` | `SHOW GRANTS` | `SHOW ROLES` | `SHOW ROLE GRANTS` | `UPDATE` | `DROP TABLE` | `CREATE ROLE` | `CREATE VIEW` | `DROP SCHEMA` | `DROP VIEW` |
| :-------------- | :-------------: | :-------------:| :-------------:| :-------------:| :-------------: | :-------------: | :-------------: | :-------------: | :-------------: | :-------------:| :-------------:| :-------------: | :-------------: | :-------------: | :-------------: | :-------------: | :-------------: | :-------------: | :-------------: |
|**Iceberg**| ✓    | ✓   | ✓  | ✓  | ✓  | ✓  | `X`   | ✓  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | ✓  | `X`  |
|**MySQL**| `X`    | ✓  | ✓  | ✓  | ✓  | `X`  | `X`   | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | ✓   | `X`  | `X`  | `X`  | `X`  |
|**PostgreSQL**| `X`    | ✓   | ✓  | ✓  | ✓  | ✓  | `X`   | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | `X`  |
|**MongoDB**| `X`    | ✓   | ✓  | ✓  | ✓  | ✓  | `X`   | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | `X`  |
|**Hive**| ✓    | ✓   | ✓  | ✓  | ✓  | `X`  | `X`   | ✓  | ✓  | ✓  | `X`    | ✓  | ✓  | `X`  | ✓  | ✓  | ✓  | ✓  | ✓  |
|**Kafka**| `X`    | `X`   | `X`  | ✓  | ✓  | `X`  | `X`   | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
| **Memory**| ✓    | ✓   | ✓  | ✓  | ✓  | `X`  | `X`   | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | ✓  | `X`  | ✓  | ✓  | ✓  |
|**TPCH**| `X`    | `X`   | `X`  | ✓  | ✓  | `X`  | `X`   | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
|**TPCDS**| `X`    | `X`   | `X`  | ✓  | ✓  | `X`  | `X`   | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
| **System**| `X`    | `X`   | `X`  | ✓  | ✓  | `X`  | `X`   | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
| **JMX**| `X`    | `X`   | `X`  | ✓  | ✓  | `X`  | `X`   | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
|**Db2**| ✓    | ✓   | ✓  | ✓  |  -- | ✓  | `X`   | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | ✓  | `X`  | ✓  | ✓  | `X`  |
|**{{site.data.keyword.netezza_short}}**| ✓    | ✓   | ✓  | ✓  |  -- | ✓  | `X`   | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | ✓  | `X`  | ✓  | ✓  | X  |
{: caption="Table 1. SQL statements and supporting connectors" caption-side="bottom"}

## Limitations
{: #connector_limitations}

1. For `CREATE TABLE`, **MySQL** connector supports only `CREATE TABLE AS`.
2. For `ALTER TABLE`, **MongoDB** connector supports only table rename.
3. **Db2** connector partially supports `ALTER TABLE`, `CREATE VIEW`, and `DROP SCHEMA`.
4. **{{site.data.keyword.netezza_short}}** connector partially supports `ALTER TABLE` and `CREATE VIEW`.
5. **MySQL**, **PostgreSQL**, **MongoDB**, **Db2**, and **{{site.data.keyword.netezza_short}}** connectors support `DROP TABLE` only when enabled in catalog.
6. The `CREATE SCHEMA`, `CREATE TABLE`, `DROP SCHEMA`, `DROP TABLE`, `DELETE`, `DROP VIEW`, `ALTER TABLE`, and `ALTER SCHEMA` are not available for database based catalogs in the **Data Manager** UI.
