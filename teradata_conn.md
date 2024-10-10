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

# Teradata
{: #teradata_database}

Teradata is a relational database management system.
{: shortdesc}

 Configure the following details for Teradata data source:

 | Field           | Description        |
 |------------------|--------------------|
 | Display name    | Enter the data source name to be displayed on the screen. |
 | Database name     | Enter the name of your database.|
 | Hostname            | Enter the hostname.  |
 | Port             | Enter the port number. |
 | Authentication type   | Choose and enter the Authentication type details. \n * TD2: Enter the username and password. \n * LDAP: Enter the username and password. |
 | Port is SSL enabled     | Use the toggle switch to enable or disable SSL connection. If enabled,  \n i. The Upload SSL certificate (.pem, .crt, .cert or .cer) link is enabled. \n ii. Click the Upload SSL certificate (.pem, .crt, .cert or .cer) link. \n iii. Browse the SSL certificate and upload.|
 | Catalog name | Enter the name of the catalog. This catalog is automatically associated with your data source. |
 | Create | Click Create to create the data source. |
 {: caption="Register data source" caption-side="bottom"}

## Limitations for SQL statements
{: #connector_limitations}

1. Only `ADD COLUMN` and `DROP COLUMN` are supported for `ALTER TABLE` statement. `DROP COLUMN` does not drop the first column.
2. `DROP TABLE` statement is supporetd only when enabled in the catalog.


## Limitations for data types
{: #connector_limitations2}

1. `BLOB` and `CLOB` data types support only `SELECT` and `CREATE` statements.
2. The data shown from the UI for `BLOB` data type is in Base64 format, while the result from presto-cli is in hexadecimal format.
3. `BINARY` data type supports only `SELECT` statement.
4. `VARBYTE` is the `BINARY` alternative data type.
5. When the fields of data type `REAL` have 6 digits or more in the decimal part with the digits being predominately zero, the values when queried are rounded off. It is observed that the rounding off occurs differently based on the precision of the values. For example, a decimal number 1.654 when rounded to 3-digits after decimal point are the same. Another example, is 10.890009 and 10.89000. It is noticed that 10.89000 is rounded to 10.89, whereas 10.89009 is not rounded off. This is an inherent issue because of the representational limitations of binary floating point formats. This might have a significant impact when querying involves sorting.
