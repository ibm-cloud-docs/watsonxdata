---

copyright:
  years: 2022, 2024
lastupdated: "2024-04-03"

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

# Data types supported in {{site.data.keyword.lakehouse_full}} for Presto
{: #supported_datatypes}


The following data types are supported in {{site.data.keyword.lakehouse_full}} for Presto through different connectors.
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
| `VARCHAR` | `X`    | ✓   | ✓  | ✓  | `X`   | ✓  | ✓   | `X`  | ✓  | `X`  | `X`  | `X`  | `X`  | `X`  | ✓  |
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
| `CLOB` | ✓    | `X`   | `X`  | ✓  | `X`   | ✓  | ✓   | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | `X`  | ✓  |
| `BLOB` | ✓    | `X`   | `X`  | ✓  | `X`   | ✓  | ✓   | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  | `X`  | ✓  |
| `BINARY` | `X`    | `X`   | `X`  | ✓  | `X`   | ✓  | `X`   | `X`  | `X`  | `X`  | `X`  | ✓  | `X`  | `X`  | `X`  |
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

For **Iceberg** connector, `ALTER TABLE` operations on a column support data type conversions from:
    `INT` to `BIGINT`
    `FLOAT` to `DOUBLE`
    `DECIMAL` (num1, dec_digits) to `DECIMAL` (num2, dec_digits), where num2>num1.
{: note}

## Limitations
{: #connector_limitations}

1. For **Teradata** connector, `BLOB` and `CLOB` data types support only `SELECT` and `CREATE` statements.
2. For **MySQL**, **Db2**, **PostgreSQL**, **Snowflake** and **SQL server** connectors, `BLOB` and `CLOB` data types support only `SELECT` statement.
3. For **MySQL**, **Oracle**, **Kudu**, **Elasticsearch** and **SQL server** connectors, `BINARY` data type supports only `SELECT` statement.
4. For **Iceberg** connector, the maximum number of digits that can be accommodated in a column of data type FLOAT and DOUBLE is 37. Trying to insert anything larger ends up in Decimal overflow error.
5. For **MySQL**, **PostgreSQL**, **Snowflake**, **SQL Server** , **Teradata** and **Db2** connectors, the data shown from the UI for `BLOB` data type is in Base64 format, while the result from presto-cli is in hexadecimal format.
6. For **MySQL** and **SQL Server** connectors, the data shown from the UI for `BINARY` data type is in Base64 format, while the result from presto-cli is in hexadecimal format.
7. When the fields of data type `REAL` have 6 digits or more in the decimal part with the digits being predominately zero, the values when queried are rounded off. It is observed that the rounding off occurs differently based on the precision of the values. For example, a decimal number 1.654 when rounded to 3-digits after decimal point will be the same. Another example, is 10.890009 and 10.89000. It is noticed that 10.89000 is rounded to 10.89, where as 10.89009 is not rounded off. This is an inherent issue because of the representational limitations of binary floating point formats. This might have a significant impact when querying involves sorting.

For more information on supported SQL statements, see [Supported SQL statements](watsonxdata?topic=watsonxdata-supported_sql_statements){: external}.
