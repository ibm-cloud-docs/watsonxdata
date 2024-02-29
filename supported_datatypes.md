---

copyright:
  years: 2022, 2024
lastupdated: "2024-02-28"

keywords: lakehouse, data types, connectors, watsonx.data

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

# Supported data types
{: #supported_datatypes}


The following data types are supported in {{site.data.keyword.lakehouse_full}} through different connectors.
{: shortdesc}

| Data types |**Db2**|**Hive**|**Iceberg**|**MySQL**|**{{site.data.keyword.netezza_short}}**|**SQL Server**|**PostgreSQL**|**SingleStore**|**MongoDB**|**Teradata**|**Kafka**|**Elasticsearch**|**TPCH**|**TPCDS**|**Snowflake**|
| :-------------- | :-------------: | :-------------:| :-------------:| :-------------:| :-------------: | :-------------: | :-------------: | :-------------: | :-------------: | :-------------:| :-------------:| :-------------: | :-------------: | :-------------: | :-------------: |
| `TINYINT` | `X`    | ✓   | `X`  | ✓  | `X`  | ✓  | `X`   | ✓  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | ✓  |
| `SAMLLINT` | ✓    | ✓  |`X`  | ✓  | ✓  | ✓  | ✓   | ✓  | `X`  | ✓  | `X`  | `X`  | `X`  | `X`  | ✓  |
| `INTEGER` | ✓    | ✓   | ✓  | ✓  | ✓  | ✓  | ✓   | ✓  | ✓  | ✓  | `X`  | `X`  | `X`  | `X`  | ✓  |
| `BIGINT` | ✓    | ✓   | ✓  | ✓  | ✓  | ✓  | ✓   | ✓  | ✓  | ✓  | `X`  | `X`  | `X`  | `X`  | ✓  |
| `REAL` | ✓    | ✓   | ✓  | ✓  | ✓  | ✓  | ✓   | ✓  | `X`  | ✓  | `X`  | `X`  | `X`  | `X`  | ✓  |
| `DOUBLE` | ✓    | ✓   | ✓  | ✓  | ✓  | ✓  | ✓   | ✓  | ✓  | ✓  | `X`  | `X`  | `X`  | `X`  | ✓  |
| `DECIMAL` | ✓    | ✓   | ✓  | ✓  | ✓  | ✓  | ✓   | ✓  | `X`  | ✓  | `X`  | `X`  | `X`  | `X`  | ✓  |
| `VARCHAR` | `X`    | ✓   | ✓  | ✓  | ✓  | ✓  | ✓   | `X`  | ✓  | `X`  | `X`  | `X`  | `X`  | `X`  | ✓  |
| `VARCHAR(n)` | ✓    | ✓   | ✓  | ✓  | ✓  | ✓  | ✓   | ✓  | ✓  | ✓  | `X`  | `X`  | `X`  | `X`  | ✓  |
| `CHAR` | ✓    | ✓   | ✓  | ✓  | ✓  | ✓  | ✓   | ✓  | ✓  | ✓  | `X`  | `X`  | `X`  | `X`  | ✓  |
| `VARBINARY (VARBINARY(n) not supported)` | `X`    | ✓   | ✓  | ✓  |`X`  | `X`  | `X`   | `X`  | ✓  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
| `JSON` | `X`    | `X`   | `X`  | `X`  | `X`  | `X`  | ✓   | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
| `DATE` | ✓    | ✓   | ✓  | ✓  | ✓  | ✓  | ✓   | ✓  | ✓  | ✓  | `X`  | `X`  | `X`  | `X`  | ✓  |
| `TIME` | ✓    | `X`   | ✓  | ✓  | ✓  | ✓  | ✓   | ✓  | ✓  | ✓  | `X`  | `X`  | `X`  | `X`  | ✓  |
| `TIME WITH TIMEZONE` | `X`    | `X`   | `X`  | `X`  | `X`  | `X`  | `X`   | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
| `TIMESTAMP` | ✓    | ✓   | ✓  | ✓  | ✓  | `X`  | ✓   | ✓  | ✓  | ✓  | `X`  | `X`  | `X`  | `X`  | ✓  |
| `TIMESTAMP WITH TIMEZONE` | `X`    | `X`   | `X`  | `X`  | `X`  | `X`  | `X`   | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
| `BOOLEAN` | ✓    | ✓   | ✓  | `X`  | ✓   | `X`  | ✓   | ✓  | ✓  | `X`  | `X`  | `X`  | `X`  | `X`  | ✓  |
| `CLOB` | ✓    | `X`   | `X`  | `X`  | `X`   | `X`  | `X`   | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
| `BLOB` | ✓    | `X`   | `X`  | ✓  | `X`   | `X`  | `X`   | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
| `BINARY` | `X`    | `X`   | `X`  | `X`  | `X`   | `X`  | `X`   | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
| `XML` | `X`    | `X`   | `X`  | `X`  | `X`   | `X`  | `X`   | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
| `INTERVAL` | `X`    | `X`   | `X`  | `X`  | `X`   | `X`  | `X`   | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
| `ARRAY` | `X`    | ✓   | ✓  | `X`  | `X`   | `X`  | `X`   | `X`  | ✓  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
| `MAP` | `X`    | ✓   | ✓  | `X`  | `X`   | `X`  | `X`   | `X`  | ✓  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
| `ROW` | `X`    | ✓   | ✓  | `X`  | `X`   | `X`  | `X`   | `X`  | ✓  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
| `IPADDRESS` | `X`    | `X`   | `X`  | `X`  | `X`   | `X`  | `X`   | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
| `IPPREFIX` | `X`    | `X`   | `X`  | `X`  | `X`   | `X`  | `X`   | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
| `UUID` | `X`    | `X`   | `X`  | `X`  | `X`   | `X`  | ✓   | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
| `HyperLogLog` | `X`    | `X`   | `X`  | `X`  | `X`   | `X`  | `X`   | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
| `KHyperLogLog` | `X`    | `X`   | `X`  | `X`  | `X`   | `X`  | `X`   | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
| `SetDigest` | `X`    | `X`   | `X`  | `X`  | `X`   | `X`  | `X`   | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
| `QDigest` | `X`    | `X`   | `X`  | `X`  | `X`   | `X`  | `X`   | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
| `TDigest` | `X`    | `X`   | `X`  | `X`  | `X`   | `X`  | `X`   | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  | `X`  |
{: caption="Table 1. Data types and supporting connectors" caption-side="bottom"}

## Limitations
{: #connector_limitations}

1. For **Db2** and **Teradata** connector, `BLOB` and `CLOB` data types support only `SELECT` and `CREATE` statements.
2. For **Iceberg** connector, the maximum number of digits that can be accommodated in a column of data type FLOAT and DOUBLE is 37. Trying to insert anything larger ends up in Decimal overflow error.


For **Iceberg** connector, `ALTER TABLE` operations on a column support data type conversions from `INT` to `BIGINT`, `FLOAT` to `DOUBLE` and `DECIMAL` (num1, dec_digits) to `DECIMAL` (num2, dec_digits), where num2>num1.
{: note}

For more information on supported SQL statements, see [Supported SQL statements](watsonxdata?topic=watsonxdata-supported_sql_statements){: external}.
