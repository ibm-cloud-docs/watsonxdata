---

copyright:
  years: 2022, 2024
lastupdated: "2024-08-14"

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

# Salesforce
{: #salesforce_database}

Salesforce database is used to securely sync your data in systems that are part of the Salesforce ecosystem.
{: shortdesc}

 Configure the following details for Salesforce data source:

 | Field           | Description        |
 |------------------|--------------------|
 | Display name    | Enter the data source name to be displayed on the screen. |
 | Hostname            | Enter the hostname.  |
 | Username           | Enter the  username.  |
 | Password           | Enter the password.  |
 | Port is SSL enabled     | Use the toggle switch to enable or disable SSL connection.  |
 | Connection details: Arrow Flight           |  Enter the following details for Arrow Flight service connection: \n Service hostname: Enter the service hostname. \n Port: Enter the port number. \n API key: Enter the API key. \n Token URL: Enter the token URL. \n Port is SSL enabled: Use the toggle switch to enable or disable SSL connection. \n Validate server certificate: This option can be used when the host certificate is not signed by a known certificate authority. Toggle the switch to enable or disable the server certificate validation. If enabled, \n i. The Upload SSL certificate (.pem, .crt, .cert or .cer) link is enabled. \n ii. Click the Upload SSL certificate (.pem, .crt, .cert or .cer) link. \n iii. Browse the SSL certificate and upload.  |
 | Catalog name | Enter the name of the catalog. This catalog is automatically associated with your data source. |
 | Create | Click Create to create the data source. |
 {: caption="Table 1. Register data source" caption-side="bottom"}

## Limitations for SQL statements
{: #connector_limitations}

1. For data source-based catalogs the `CREATE SCHEMA`, `CREATE TABLE`, `DROP SCHEMA`, `DROP TABLE`, `DELETE`, `DROP VIEW`, `ALTER TABLE`, and `ALTER SCHEMA` statements are not available in the **Data Manager** UI.

## Limitations for data types
{: #connector_limitations2}

1. When the fields of data type `REAL` have 6 digits or more in the decimal part with the digits being predominately zero, the values when queried are rounded off. It is observed that the rounding off occurs differently based on the precision of the values. For example, a decimal number 1.654 when rounded to 3-digits after decimal point are the same. Another example, is 10.890009 and 10.89000. It is noticed that 10.89000 is rounded to 10.89, whereas 10.89009 is not rounded off. This is an inherent issue because of the representational limitations of binary floating point formats. This might have a significant impact when querying involves sorting.
