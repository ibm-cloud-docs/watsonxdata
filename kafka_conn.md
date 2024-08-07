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

# Apache Kafka
{: #kafka_database}

Apache Kafka is a distributed event streaming platform. Connect to an Apache Kafka real-time processing server to write and to read Streams of events from and into topics.
{: shortdesc}


 If you select **Apache Kafka** from the **Database type** drop-down list, configure the following details:

 | Field           | Description        |
 |------------------|--------------------|
 | Display name    | Enter the database name to be displayed on the screen. |
 | Hostname            | Enter the hostname. You can add multiple host information. To add, click the **Add** icon. A new row appears for adding hostname and port. Enter the details.  |
 | Port             | Enter the port number. |
 | SASL connection   | Enable the Simple Authentication Security Layer (SASL) to include authentication mechanism. If you enable SASL, specify the username and API key/password.|
 | Test connection     | Click the Test connection link to test the database connection. If the database connection is successful, a success message appears.|
 | Catalog name | Enter the name of the catalog. This catalog is automatically associated with your database. |
 | Add topics    | You can add topics after you create the database.  \n i. Go to the **Infrastructure manager**. \n ii. Click on the **Apache Kafka** database. \n iii. Click **Add topics** option. \n iv. Upload .json definition files. You can either drag the files or use the **Click to upload** option. Topic names are determined from the definition files. \n v. Use the **Edit** option to view and edit the topic files.|
 | Create | Click Create to create the database. |
 {: caption="Table 1. Register database" caption-side="bottom"}


## Limitations for SQL statements
{: #connector_limitations}

1. For database-based catalogs the `CREATE SCHEMA`, `CREATE TABLE`, `DROP SCHEMA`, `DROP TABLE`, `DELETE`, `DROP VIEW`, `ALTER TABLE`, and `ALTER SCHEMA` statements are not available in the **Data Manager** UI.

## Limitations for data types
{: #connector_limitations2}

1. When the fields of data type `REAL` have 6 digits or more in the decimal part with the digits being predominately zero, the values when queried are rounded off. It is observed that the rounding off occurs differently based on the precision of the values. For example, a decimal number 1.654 when rounded to 3-digits after decimal point are the same. Another example, is 10.890009 and 10.89000. It is noticed that 10.89000 is rounded to 10.89, whereas 10.89009 is not rounded off. This is an inherent issue because of the representational limitations of binary floating point formats. This might have a significant impact when querying involves sorting.
