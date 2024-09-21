---

copyright:
  years: 2022, 2024
lastupdated: "2024-09-18"

keywords: lakehouse, bucket, catalog, watsonx.data

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

# Apache Ozone
{: #ozone_storage}

Apache Ozone Storage stores encrypted and dispersed data across multiple geographic locations..
{: shortdesc}

If you select **Apache Ozone** from the **Storage** section, configure the following details:

 | Field | Description |
 |--------------------------|----------------|
 | Display name | Enter the name to be displayed.|
 | Bucket name | Enter your existing object storage bucket name.|
 | Endpoint | Enter the endpoint URL.|
 | Access key | Enter your access key. |
 | Secret key | Enter your secret key. |
 | Connection Status | Click the Test connection link to test the storage connection. If the connection is successful, a success message appears.|
 | Associate catalog | Select the checkbox to add a catalog for your storage. This catalog is automatically associated with your storage and serves as your query interface with the data stored within. |
 | Activate now| Select the checkbox to activate the storage immediately or activate it later. |
 | Catalog type | Apache Iceberg is the available catalog type.|
 | Catalog name | Enter the name of your catalog.|
 | Create | Click Create to create the storage. |
 {: caption="Table 1. Register bucket" caption-side="bottom"}
