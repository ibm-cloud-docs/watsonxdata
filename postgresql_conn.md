---

copyright:
  years: 2022, 2025
lastupdated: "2025-08-25"

keywords: lakehouse, database, watsonx.data

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

# PostgreSQL
{: #postgresql_database}

IBM Cloud Databases for PostgreSQL is an open source object-relational database that is highly customizable. It’s a feature-rich enterprise database with JSON support.
{: shortdesc}

You can configure PostgreSQL using one of the following methods:
- `Create new connection` – If you select the `Create new connection` tab, refer to the [Create new connection - configuration details](/docs/watsonxdata?topic=watsonxdata-postgresql_database#postgresql_database1) table to provide configuration details.

- `Import from catalog` – You can import connection details from an existing catalog in the data platform. If you select the `Import from catalog` tab, refer to the [Import from catalog - configuration details](/docs/watsonxdata?topic=watsonxdata-postgresql_database#postgresql_database2) table to provide configuration details.

- `Import from project` – You can import connection details from an existing project in the data platform. If you select `Import from project`, refer to the [Import from project - configuration details](/docs/watsonxdata?topic=watsonxdata-postgresql_database#postgresql_database3) table to provide configuration details.

## Create new connection - configuration details
{: #postgresql_database1}

 | Field           | Description        |
 |------------------|--------------------|
 | Display name    | Enter the database name to be displayed on the screen. |
 | Database name     | Enter the name of your database.|
 | Hostname            | Enter the hostname.  |
 | Port             | Enter the port number. |
 | Username           | Enter the username.  |
 | Password           | Enter the password.  |
 | Port is SSL enabled   | Use the toggle switch to enable or disable SSL connection. If enabled, \n i. The Upload SSL certificate (.pem, .crt, .cert or .cer) link is enabled. \n ii. Click the Upload SSL certificate (.pem, .crt, .cert or .cer) link. \n iii. Browse the SSL certificate and upload.|
 | Validate certificate           | The toggle switch must be enabled to Validate certificate. If disabled, the test connection feature does not work and the PostgreSQL database cannot be added to the engine.  |
 | Connection status    | Click the Test connection link to test the database connection. If the database connection is successful, a success message appears.|
 | Associate catalog | Select the checkbox to associate a catalog to the data source. This catalog is automatically associated with your data source and serves as your query interface with the data stored within.|
 | Catalog name | Enter the name of the catalog. |
 | Create | Click Create to create the database. |
 {: caption="Crete new connection - configuration details" caption-side="bottom"}

Enable the toggle switch for Validate certificate option to create the PostgreSQL database. If disabled, the Test connection feature does not work and the database cannot be added to the engine.
{: note}

## Import from catalog - configuration details
{: #postgresql_database2}

 | Field | Description |
| --- | --- |
| Select catalog | Use the dropdown to select a catalog. |
| Select data source | Use the dropdown to select a data source from the selected catalog. |
| Connection status | Click the Test connection link to test the database connection. If the database connection is successful, a success message appears. |
| Display name | Enter the database name to be displayed on the screen. |
| Associate catalog | Select the checkbox to associate a catalog to the data source. This catalog is automatically associated with your data source and serves as your query interface with the data stored within. |
| Catalog name | Enter the name of the catalog. |
| Create | Click Create to create the database. |
{: caption="Import from catalog - configuration details" caption-side="bottom"}


## Import from project - configuration details
{: #postgresql_database3}

| Field | Description |
| --- | --- |
| Select project | Use the dropdown to select a project. |
| Select data source | Use the dropdown to select a data source from the selected project |
| Connection status | Click the Test connection link to test the database connection. If the database connection is successful, a success message appears. |
| Display name | Enter the database name to be displayed on the screen. |
| Associate catalog | Select the checkbox to associate a catalog to the data source. This catalog is automatically associated with your data source and serves as your query interface with the data stored within. |
| Catalog name | Enter the name of the catalog. |
| Create | Click Create to create the database. |
{: caption="Import from project - configuration details" caption-side="bottom"}

## Limitations for SQL statements
{: #connector_limitations}

* `DROP TABLE` statement is supported only when enabled in the catalog.
* For database-based catalogs the `CREATE SCHEMA`, `CREATE TABLE`, `DROP SCHEMA`, `DROP TABLE`, `DELETE`, `DROP VIEW`, `ALTER TABLE`, and `ALTER SCHEMA` statements are not available in the **Data Manager** UI.

## Limitations for data types
{: #connector_limitations2}

* `BLOB` and `CLOB` data types can be used as an equivalent alternative to `BYTEA` and `TEXT` respectively.
* `BLOB` and `CLOB` data types support `SELECT` statement but do not support operations such as `equal`, `like`, and `in`.
* The data that is shown from the UI for `BLOB` data type is in Base64 format, while the result from presto-cli is in hexadecimal format.
* `BINARY` data type supports only `SELECT` statement.
* `BYTEA` is the `BINARY` alternative data type.
* When the fields of data type `REAL` have 6 digits or more in the decimal part with the digits being predominately zero, the values when queried are rounded off. It is observed that the rounding off occurs differently based on the precision of the values. For example, a decimal number 1.654 when rounded to 3-digits after the decimal point are the same. Another example is 10.890009 and 10.89000. It is noticed that 10.89000 is rounded to 10.89, whereas 10.89009 is not rounded off. This is an inherent issue because of the representational limitations of binary floating point formats. This might have a significant impact when querying involves sorting.
