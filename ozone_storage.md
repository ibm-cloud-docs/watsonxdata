---

copyright:
  years: 2022, 2025
lastupdated: "2025-12-02"

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
 | Associate catalog | Enable the toggle switch to add a catalog for your storage. This catalog is automatically associated with your storage and serves as your query interface with the data stored within. |
 | Catalog type | Apache Iceberg is the available catalog type.|
 | Catalog name | Enter the name of your catalog.|
 | Base path (optional) <br> **Note:** /n This field is available only in the watsonx.data Lite instance. /n This field appears only when you select Apache Iceberg as the catalog type. | Enter the base path for the catalog in the object storage. This allows you to associate multiple Iceberg catalogs with a single storage. <br>**Note:** You cannot share a storage between Iceberg and non-Iceberg catalogs. |
 | Associate | Click Associate to create the storage. |
 {: caption="Register bucket" caption-side="bottom"}

If Apache Ozone Storage is already inactive in old instances, the system will display the `Activate` button. Once you activate Apache Ozone Storage, the system will automatically remove the `Activate` button.
{: note}

## Limitations:
{: #ozone_01storage}

* Apache Ozone storage requires three datanodes to create iceberg tables from {{site.data.keyword.lakehouse_short}}.
