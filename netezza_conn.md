---

copyright:
  years: 2022, 2025
lastupdated: "2025-10-29"

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

# IBM Netezza
{: #netezza_database}

**{{site.data.keyword.netezza_full}}** is a platform for high-performance data warehousing and analytics.
{: shortdesc}

You can configure {{site.data.keyword.netezza_short}} using one of the following methods:
- `Create new connection` – If you select the `Create new connection` tab, refer to the [Create new connection - configuration details](/docs/watsonxdata?topic=watsonxdata-netezza_database#netezza_database1) table to provide configuration details.

- `Import from catalog` – You can import connection details from an existing catalog in the data platform. If you select the `Import from catalog` tab, refer to the [Import from catalog - configuration details](/docs/watsonxdata?topic=watsonxdata-netezza_database#netezza_database2) table to provide configuration details.

- `Import from project` – You can import connection details from an existing project in the data platform. If you select `Import from project`, refer to the [Import from project - configuration details](/docs/watsonxdata?topic=watsonxdata-netezza_database#netezza_database3) table to provide configuration details.

## Create new connection - configuration details
{: #netezza_database1}

 | Field           | Description        |
 |------------------|--------------------|
 | Target persistence | Select the target persistence: \n * Watsonx.data instance - The instance console database stores the connection details exclusively. \n * Platform asset catalog - The default catalog in the data platform stores your connection details. \n You can select the `Platform asset catalog` option only if data platform services are active, a **Platform asset catalog** exists in the data platform, and you have access to it. |
 | Display name    | Enter the data source name to be displayed on the screen. |
 | Database name     | Enter the name of your database. |
 | Hostname            | Enter the hostname.  |
 | Port             | Enter the port number. |
 | Username           | Enter the username.  |
 | Password           | Enter the password.  |
 | Port is SSL enabled   | Use the toggle switch to enable or disable SSL connection. If enabled, \n i. The Upload SSL certificate (.pem, .crt, .cert or .cer) link is enabled. \n ii. Click the Upload SSL certificate (.pem, .crt, .cert or .cer) link. \n iii. Browse the SSL certificate and upload.|
 | Connection status     | Click the Test connection link to test the data source connection. If the data source connection is successful, a success message appears.|
 | Associate catalog | Select the checkbox to associate a catalog to the data source. This catalog is automatically associated with your data source and serves as your query interface with the data stored within.|
 | Catalog name | Enter the name of the catalog.|
 | Create | Click Create to create the data source. |
 {: caption="Crete new connection - configuration details" caption-side="bottom"}

 For a data source type as {{site.data.keyword.netezza_short}}, select the version 11.2.2.x.
 {: note}

## Import from catalog - configuration details
{: #netezza_database2}

 | Field | Description |
| --- | --- |
| Select catalog | Use the dropdown to select a catalog. |
| Select data source | Use the dropdown to select a data source from the selected catalog. |
| Target persistence | Select the target persistence: \n * Watsonx.data instance - The instance console database stores the connection details exclusively. \n * Platform asset catalog - The default catalog in the data platform stores your connection details. \n You can select the `Platform asset catalog` option only if data platform services are active, a **Platform asset catalog** exists in the data platform, and you have access to it. |
| Connection status | Click the Test connection link to test the database connection. If the database connection is successful, a success message appears. |
| Display name | Enter the database name to be displayed on the screen. |
| Associate catalog | Select the checkbox to associate a catalog to the data source. This catalog is automatically associated with your data source and serves as your query interface with the data stored within. |
| Catalog name | Enter the name of the catalog. |
| Create | Click Create to create the database. |
{: caption="Import from catalog - configuration details" caption-side="bottom"}


## Import from project - configuration details
{: #netezza_database3}

| Field | Description |
| --- | --- |
| Select project | Use the dropdown to select a project. |
| Select data source | Use the dropdown to select a data source from the selected project |
| Target persistence | Select the target persistence: \n * Watsonx.data instance - The instance console database stores the connection details exclusively. \n * Platform asset catalog - The default catalog in the data platform stores your connection details. \n You can select the `Platform asset catalog` option only if data platform services are active, a **Platform asset catalog** exists in the data platform, and you have access to it. |
| Connection status | Click the Test connection link to test the database connection. If the database connection is successful, a success message appears. |
| Display name | Enter the database name to be displayed on the screen. |
| Associate catalog | Select the checkbox to associate a catalog to the data source. This catalog is automatically associated with your data source and serves as your query interface with the data stored within. |
| Catalog name | Enter the name of the catalog. |
| Create | Click Create to create the database. |
{: caption="Import from project - configuration details" caption-side="bottom"}



## Limitations for SQL statements
{: #connector_limitations}

* `DROP TABLE` statement is supported only when enabled in the catalog.
* `CREATE VIEW` can be used for a table only if that table is in the same catalog.
* `DROP TABLE` statement is supported only when enabled in the catalog.
* For data source-based catalogs the `CREATE SCHEMA`, `CREATE TABLE`, `DROP SCHEMA`, `DROP TABLE`, `DELETE`, `DROP VIEW`, `ALTER TABLE`, and `ALTER SCHEMA` statements are not available in the **Data Manager** UI.
* In the `CREATE VIEW` statement, column names must be enclosed in double quotes, and their case must match precisely as they are stored in the database, including uppercase, lowercase, or mixed case.

## Limitations for data types
{: #connector_limitations2}

* `NUMERIC` data type is not supported. You can use `DECIMAL` data type as an equivalent alternative to `NUMERIC` data type.
* When the fields of data type `REAL` have 6 digits or more in the decimal part with the digits being predominately zero, the values when queried are rounded off. It is observed that the rounding off occurs differently based on the precision of the values. For example, a decimal number 1.654 when rounded to 3-digits after the decimal point are the same. Another example is 10.890009 and 10.89000. It is noticed that 10.89000 is rounded to 10.89, whereas 10.89009 is not rounded off. This is an inherent issue because of the representational limitations of binary floating point formats. This might have a significant impact when querying involves sorting.

 **{{site.data.keyword.netezza_short}}** supports the unicode characters from the Presto (Java) engine with varchar and char data types.
 {: note}
