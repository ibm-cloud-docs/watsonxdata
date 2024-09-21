---

copyright:
  years: 2022, 2024
lastupdated: "2024-09-21"

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

# Apache Kafka
{: #kafka_database}

Apache Kafka is a distributed event streaming platform. Connect to an Apache Kafka real-time processing server to write and to read Streams of events from and into topics.
{: shortdesc}


 Configure the following details for Apache Kafka data source:

 | Field           | Description        |
 |------------------|--------------------|
 | Display name    | Enter the data source name to be displayed on the screen. |
 | Hostname            | Enter the hostname. You can add multiple host information. To add, click the **Add** icon. A new row appears for adding hostname and port. Enter the details.  |
 | Port             | Enter the port number. |
 | SASL connection   | Use the toggle switch to enable or disable the Simple Authentication Security Layer (SASL) to include an authentication mechanism. If enabled, \n 1. Upload the SSL certificate: \n i. The Upload SSL certificate (.pem, .crt, .cert, or .cer) link is enabled. \n ii. Click the Upload SSL certificate (.pem, .crt, .cert, or .cer) link. \n iii. Browse the SSL certificate and upload. \n 2. Select one of the following SASL mechanisms: \n * PLAIN \n * SCRAM SHA-256 \n * SCRAM SHA-512 \n 3. Enter the Username and API key/Password.|
 | Test connection     | Click the Test connection link to test the data source connection. If the data source connection is successful, a success message appears. This feature is not applicale with SASL mechanism enabled.|
 | Catalog name | Enter the name of the catalog. This catalog is automatically associated with your data source. |
 | Add topics    | You can add topics after you create the data source.  \n i. Go to the **Infrastructure manager**. \n ii. Click on the **Apache Kafka** data source. \n iii. Click **Add topics** option. \n iv. Upload .json definition files. You can either drag the files or use the **Click to upload** option. Topic names are determined from the definition files. \n v. Use the **Edit** option to view and edit the topic files.|
 | Create | Click Create to create the data source. |
 {: caption="Table 1. Register data source" caption-side="bottom"}


## Limitations for SQL statements
{: #connector_limitations}

1. For data source-based catalogs the `CREATE SCHEMA`, `CREATE TABLE`, `DROP SCHEMA`, `DROP TABLE`, `DELETE`, `DROP VIEW`, `ALTER TABLE`, and `ALTER SCHEMA` statements are not available in the **Data Manager** UI.

## Limitations for data types
{: #connector_limitations2}

1. When the fields of data type `REAL` have 6 digits or more in the decimal part with the digits being predominately zero, the values when queried are rounded off. It is observed that the rounding off occurs differently based on the precision of the values. For example, a decimal number 1.654 when rounded to 3-digits after decimal point are the same. Another example, is 10.890009 and 10.89000. It is noticed that 10.89000 is rounded to 10.89, whereas 10.89009 is not rounded off. This is an inherent issue because of the representational limitations of binary floating point formats. This might have a significant impact when querying involves sorting.
