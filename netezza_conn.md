---

copyright:
  years: 2022, 2024
lastupdated: "2024-10-10"

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

# IBM {{site.data.keyword.netezza_short}}
{: #netezza_database}

**{{site.data.keyword.netezza_short}}** is a platform for high-performance data warehousing and analytics.
{: shortdesc}

 Configure the following details for {{site.data.keyword.netezza_short}} data source:

 | Field           | Description        |
 |------------------|--------------------|
 | Display name    | Enter the data source name to be displayed on the screen. |
 | Database name     | Enter the name of your database. |
 | Hostname            | Enter the hostname.  |
 | Port             | Enter the port number. |
 | Username           | Enter the  username.  |
 | Password           | Enter the password.  |
 | Port is SSL enabled   | Use the toggle switch to enable or disable SSL connection. If enabled, \n i. The Upload SSL certificate (.pem, .crt, .cert or .cer) link is enabled. \n ii. Click the Upload SSL certificate (.pem, .crt, .cert or .cer) link. \n iii. Browse the SSL certificate and upload.|
 | Test connection     | Click the Test connection link to test the data source connection. If the data source connection is successful, a success message appears.|
 | Catalog name | Enter the name of the catalog. This catalog is automatically associated with your data source. |
 | Create | Click Create to create the data source. |
 {: caption="Register data source" caption-side="bottom"}

 For a data source type as {{site.data.keyword.netezza_short}}, select the version 11.2.2.x.
 {: note}


## Limitations for SQL statements
{: #connector_limitations}

1. `ALTER TABLE` and `CREATE VIEW` statements are partially supported.
2. `DROP TABLE` statement is supported only when enabled in the catalog.
3. `CREATE VIEW` can be used for a table only if that table is in the same catalog and the same schema.
4. `DROP TABLE` statement is supported only when enabled in the catalog.
5. For data source-based catalogs the `CREATE SCHEMA`, `CREATE TABLE`, `DROP SCHEMA`, `DROP TABLE`, `DELETE`, `DROP VIEW`, `ALTER TABLE`, and `ALTER SCHEMA` statements are not available in the **Data Manager** UI.

## Limitations for data types
{: #connector_limitations2}

1. `NUMERIC` data type is not supported. You can use `DECIMAL` data type as an equivalent alternative to `NUMERIC` data type.
2. When the fields of data type `REAL` have 6 digits or more in the decimal part with the digits being predominately zero, the values when queried are rounded off. It is observed that the rounding off occurs differently based on the precision of the values. For example, a decimal number 1.654 when rounded to 3-digits after decimal point are the same. Another example, is 10.890009 and 10.89000. It is noticed that 10.89000 is rounded to 10.89, whereas 10.89009 is not rounded off. This is an inherent issue because of the representational limitations of binary floating point formats. This might have a significant impact when querying involves sorting.

 **{{site.data.keyword.netezza_short}}** supports the unicode characters from the Presto (Java) engine with varchar and char data types.
 {: note}
