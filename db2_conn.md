---

copyright:
  years: 2022, 2025
lastupdated: "2025-08-25"

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

# IBM Db2
{: #db2_database}

IBM Db2 is a data source that contains relational data.
{: shortdesc}

You can configure IBM Db2 using one of the following methods:
- `Create new connection` – If you select the `Create new connection` tab, refer to the [Create new connection - configuration details](/docs/watsonxdata?topic=watsonxdata-db2_database#db2_database1) table to provide configuration details.

- `Import from catalog` – You can import connection details from an existing catalog in the data platform. If you select the `Import from catalog` tab, refer to the [Import from catalog - configuration details](/docs/watsonxdata?topic=watsonxdata-db2_database#db2_database2) table to provide configuration details.

- `Import from project` – You can import connection details from an existing project in the data platform. If you select `Import from project`, refer to the [Import from project - configuration details](/docs/watsonxdata?topic=watsonxdata-db2_database#db2_database3) table to provide configuration details.

## Create new connection - configuration details
{: #db2_database1}

 | Field           | Description        |
 |------------------|--------------------|
 | Display name    | Enter the data source name to be displayed on the screen. |
 | Database name     | Enter the name of your database. |
 | Hostname            | Enter the hostname.  |
 | Port             | Enter the port number. |
 | Authentication type   | Choose and enter the Authentication type details. \n * Username and password: Enter the username and password. \n * API key: Enter the API key. |
 | Port is SSL enabled   | Use the toggle switch to enable or disable SSL connection. If enabled, \n i. The Upload SSL certificate (.pem, .crt, .cert or .cer) link is enabled. \n ii. Click the Upload SSL certificate (.pem, .crt, .cert or .cer) link. \n iii. Browse the SSL certificate and upload.|
 | Connection Status    | Click the Test connection link to test the data source connection. If the data source connection is successful, a success message appears.|
 | Associate catalog | Select the checkbox to associate a catalog to the data source. This catalog is automatically associated with your data source and serves as your query interface with the data stored within.|
 | Catalog name | Enter the name of the catalog.|
 | Create | Click Create to create the data source. |
 {: caption="Crete new connection - configuration details" caption-side="bottom"}

## Import from catalog - configuration details
{: #db2_database2}

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
{: #db2_database3}

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

 Select IBM Db2 from the data source section to add IBM Watson Query.
 You can now query the nicknames that are created in IBM Db2 and the virtualized tables from Watson Query instances.
{: note}

## Features
{: #features_connectors}

* You can perform the following operations for `BLOB` and `CLOB` data types for IBM Db2 data source:

   * INSERT
   * CREATE
   * CTAS
   * ALTER
   * DROP

* To insert `CLOB` data type, provide the value directly or cast it explicitly to `CLOB` data type.

   ```bash
   INSERT INTO <table_name> VALUES ('<clob value>', '<other values>');
   INSERT INTO <table_name> VALUES (CAST('<clob text>' AS CLOB));
   ```
   {: codeblock}

* To insert `BLOB` data, use the cast function with `BLOB` data type. The corresponding hexadecimal value is inserted into the IBM Db2 data source:

   ```bash
   INSERT INTO <table_name> VALUES (CAST('<blob text>' AS BLOB));
   ```
   {: codeblock}

## Limitations for SQL statements
{: #connector_limitations}

* `ALTER TABLE DROP COLUMN` operation is not supported for column-organized tables.
* `DROP TABLE` statement is supported only when enabled in the catalog.
* `CREATE VIEW` can be used for a table only if that table is in the same catalog.
* `DROP SCHEMA` can do `RESTRICT` by default.
* For data source-based catalogs the `CREATE SCHEMA`, `CREATE TABLE`, `DROP SCHEMA`, `DROP TABLE`, `DELETE`, `DROP VIEW`, `ALTER TABLE`, and `ALTER SCHEMA` statements are not available in the **Data Manager** UI.
* In the `CREATE VIEW` statement, column names must be enclosed in double quotes, and their case must match exactly as they are stored in the database, including uppercase, lowercase, or mixed case.
* The `ALTER VIEW RENAME` operation is not supported.

## Limitations for data types
{: #connector_limitations2}

* `BLOB` and `CLOB` data types support `SELECT` statement but do not support operations such as `equal`, `like`, and `in`.
* `BINARY` data type supports only `SELECT` statement.
* When the fields of data type `REAL` have 6 digits or more in the decimal part with the digits being predominately zero, the values when queried are rounded off. It is observed that the rounding off occurs differently based on the precision of the values. For example, a decimal number 1.654 when rounded to 3-digits after the decimal point are the same. Another example is 10.890009 and 10.89000. It is noticed that 10.89000 is rounded to 10.89, whereas 10.89009 is not rounded off. This is an inherent issue because of the representational limitations of binary floating point formats. This might have a significant impact when querying involves sorting.
