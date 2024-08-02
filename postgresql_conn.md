---

copyright:
  years: 2022, 2024
lastupdated: "2024-08-02"

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

 If you select **PostgreSQL** from the **Database type** drop-down list, configure the following details:

 | Field           | Description        |
 |------------------|--------------------|
 | Display name    | Enter the database name to be displayed on the screen. |
 | Database name     | Enter the name of your database.|
 | Hostname            | Enter the hostname.  |
 | Port             | Enter the port number. |
 | Username           | Enter the  username.  |
 | Password           | Enter the password.  |
 | Port is SSL enabled   | Use the toggle switch to enable or disable SSL connection. If enabled, \n i. The Upload SSL certificate (.pem, .crt, .cert or .cer) link is enabled. \n ii. Click the Upload SSL certificate (.pem, .crt, .cert or .cer) link. \n iii. Browse the SSL certificate and upload.|
 | Validate certificate           | Use the toggle switch to validate whether the SSL certificate that is returned by the host is trusted or not.  |
 | Test connection     | Click the Test connection link to test the database connection. If the database connection is successful, a success message appears.|
 | Catalog name | Enter the name of the catalog. This catalog is automatically associated with your database. |
 | Create | Click Create to create the database. |
 {: caption="Table 1. Register database" caption-side="bottom"}

## Limitations for SQL statements
{: #connector_limitations}

1. `DROP TABLE` statement is supported only when enabled in the catalog.
2. For database-based catalogs the `CREATE SCHEMA`, `CREATE TABLE`, `DROP SCHEMA`, `DROP TABLE`, `DELETE`, `DROP VIEW`, `ALTER TABLE`, and `ALTER SCHEMA` statements are not available in the **Data Manager** UI.

## Limitations for data types
{: #connector_limitations2}

1. `BLOB` and `CLOB` data types can be used as an equivalent alternative to `BYTEA` and `TEXT` respectively.
2. `BLOB` and `CLOB` data types support `SELECT` statement but do not support operations such as `equal`, `like`, and `in`.
3. The data that is shown from the UI for `BLOB` data type is in Base64 format, while the result from presto-cli is in hexadecimal format.
4. `BINARY` data type supports only `SELECT` statement.
5. `BYTEA` is the `BINARY` alternative data type.
6. When the fields of data type `REAL` have 6 digits or more in the decimal part with the digits being predominately zero, the values when queried are rounded off. It is observed that the rounding off occurs differently based on the precision of the values. For example, a decimal number 1.654 when rounded to 3-digits after decimal point are the same. Another example, is 10.890009 and 10.89000. It is noticed that 10.89000 is rounded to 10.89, whereas 10.89009 is not rounded off. This is an inherent issue because of the representational limitations of binary floating point formats. This might have a significant impact when querying involves sorting.
