---

copyright:
  years: 2022, 2025
lastupdated: "2025-10-26"

keywords: lakehouse, data source, watsonx.data

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

# Snowflake
{: #snowflake_database}

Snowflake is a cloud-hosted relational database for building data warehouse.
{: shortdesc}

You can configure Snowflake using one of the following methods:
- `Create new connection` – If you select the `Create new connection` tab, refer to the [Create new connection - configuration details](/docs/watsonxdata?topic=watsonxdata-snowflake_database#snowflake_database1) table to provide configuration details.

- `Import from catalog` – You can import connection details from an existing catalog in the data platform. If you select the `Import from catalog` tab, refer to the [Import from catalog - configuration details](/docs/watsonxdata?topic=watsonxdata-snowflake_database#snowflake_database2) table to provide configuration details.

- `Import from project` – You can import connection details from an existing project in the data platform. If you select `Import from project`, refer to the [Import from project - configuration details](/docs/watsonxdata?topic=watsonxdata-snowflake_database#snowflake_database3) table to provide configuration details.

## Create new connection - configuration details
{: #snowflake_database1}

 | Field           | Description        |
 |------------------|--------------------|
 | Target persistence | Select the target persistence: \n * Watsonx.data instance - The instance console database stores the connection details exclusively. \n * Platform asset catalog - The default catalog in the data platform stores your connection details. If you select Platform asset catalog as the target persistence, you must specify a warehouse name.\n You can enable the Platform asset catalog option only if data platform services are active, a **Platform asset catalog** exists in the data platform, and you have access to it. |
 | Display name    | Enter the data source name to be displayed on the screen. |
 | Database name     | Enter the name of your database.|
 | Account name            | Enter your Snowflake Account name. This may include region information (For example, account_name.region_id). If you do not have region information, use the account name that is provided by your Snowflake administrator.  |
 | Warehouse name (optional)         | Enter the Warehouse name.  |
 | Username           | Enter the username.  |
 | Password           | Enter the password.  |
 | Connection status   | Click the Test connection link to test the database connection. If the database connection is successful, a success message appears. |
 | Associate catalog  | Select the checkbox to associate a catalog to the data source. This catalog is automatically associated with your data source and serves as your query interface with the data stored within. |
 | Catalog name | Enter the name of the catalog. |
 | Create | Click Create to create the data source. |
 {: caption="Crete new connection - configuration details" caption-side="bottom"}

## Import from catalog - configuration details
{: #snowflake_database2}

 | Field | Description |
| --- | --- |
| Select catalog | Use the dropdown to select a catalog. |
| Target persistence | Select the target persistence: \n * Watsonx.data instance - The instance console database stores the connection details exclusively. \n * Platform asset catalog - The default catalog in the data platform stores your connection details. \n You can enable the Platform asset catalog option only if data platform services are active, a **Platform asset catalog** exists in the data platform, and you have access to it. |
| Select data source | Use the dropdown to select a data source from the selected catalog. |
| Connection status | Click the Test connection link to test the database connection. If the database connection is successful, a success message appears. |
| Display name | Enter the database name to be displayed on the screen. |
| Associate catalog | Select the checkbox to associate a catalog to the data source. This catalog is automatically associated with your data source and serves as your query interface with the data stored within. |
| Catalog name | Enter the name of the catalog. |
| Create | Click Create to create the database. |
{: caption="Import from catalog - configuration details" caption-side="bottom"}


## Import from project - configuration details
{: #snowflake_database3}

| Field | Description |
| --- | --- |
| Select project | Use the dropdown to select a project. |
| Target persistence | Select the target persistence: \n * Watsonx.data instance - The instance console database stores the connection details exclusively. \n * Platform asset catalog - The default catalog in the data platform stores your connection details. \n You can enable the Platform asset catalog option only if data platform services are active, a **Platform asset catalog** exists in the data platform, and you have access to it. |
| Select data source | Use the dropdown to select a data source from the selected project |
| Connection status | Click the Test connection link to test the database connection. If the database connection is successful, a success message appears. |
| Display name | Enter the database name to be displayed on the screen. |
| Associate catalog | Select the checkbox to associate a catalog to the data source. This catalog is automatically associated with your data source and serves as your query interface with the data stored within. |
| Catalog name | Enter the name of the catalog. |
| Create | Click Create to create the database. |
{: caption="Import from project - configuration details" caption-side="bottom"}

## Limitations for SQL statements
{: #connector_limitations}

* `CREATE TABLE AS` is also supported for `CREATE TABLE` statement.
* `DROP TABLE` statement only when enabled in the catalog.
* For data source-based catalogs the `CREATE SCHEMA`, `CREATE TABLE`, `DROP SCHEMA`, `DROP TABLE`, `DELETE`, `DROP VIEW`, `ALTER TABLE`, and `ALTER SCHEMA` statements are not available in the **Data Manager** UI.

## Limitations for data types
{: #connector_limitations2}

* `BLOB` and `CLOB` data types support `SELECT` statement but do not support operations such as `equal`, `like`, and `in`.
* The data that is shown from the UI for `BLOB` data type is in Base64 format, while the result from presto-cli is in hexadecimal format.
* `BINARY` data type supports only `SELECT` statement.
* When the fields of data type `REAL` have 6 digits or more in the decimal part with the digits being predominately zero, the values when queried are rounded off. It is observed that the rounding off occurs differently based on the precision of the values. For example, a decimal number 1.654 when rounded to 3-digits after the decimal point are the same. Another example is 10.890009 and 10.89000. It is noticed that 10.89000 is rounded to 10.89, whereas 10.89009 is not rounded off. This is an inherent issue because of the representational limitations of binary floating point formats. This might have a significant impact when querying involves sorting.
