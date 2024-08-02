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

# Prometheus
{: #prometheus_database}

Prometheus allows reading Prometheus metrics as tables in Trino by using the Prometheus HTTP API mechanism.
{: shortdesc}

 If you select **Prometheus** from the **Database type** drop-down list, configure the following details:

 | Field           | Description        |
 |------------------|--------------------|
 | Display name    | Enter the database name to be displayed on the screen. |
 | Hostname            | Enter the hostname.  |
 | Port             | Enter the port number. |
 | Port is SSL enabled   | Use the toggle switch to enable or disable SSL connection. If enabled,  \n i. The Upload SSL certificate (.pem, .crt, .cert or .cer) link is enabled. \n ii. Click the Upload SSL certificate (.pem, .crt, .cert or .cer) link. \n iii. Browse the SSL certificate and upload.|
 | Verify hostname | Use the toggle switch to verify hostname in the SSL certificate. |
 | Catalog name | Enter the name of the catalog. This catalog is automatically associated with your database. |
 | Create | Click Create to create the database. |
 {: caption="Table 1. Register database" caption-side="bottom"}

## Limitations for SQL statements
{: #connector_limitations}

1. For database-based catalogs the `CREATE SCHEMA`, `CREATE TABLE`, `DROP SCHEMA`, `DROP TABLE`, `DELETE`, `DROP VIEW`, `ALTER TABLE`, and `ALTER SCHEMA` statements are not available in the **Data Manager** UI.

## Limitations for data types
{: #connector_limitations2}

1. When the fields of data type `REAL` have 6 digits or more in the decimal part with the digits being predominately zero, the values when queried are rounded off. It is observed that the rounding off occurs differently based on the precision of the values. For example, a decimal number 1.654 when rounded to 3-digits after decimal point are the same. Another example, is 10.890009 and 10.89000. It is noticed that 10.89000 is rounded to 10.89, whereas 10.89009 is not rounded off. This is an inherent issue because of the representational limitations of binary floating point formats. This might have a significant impact when querying involves sorting.
