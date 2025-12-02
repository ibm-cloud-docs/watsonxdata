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

# Google Cloud Storage
{: #gcs_storage}

Google Cloud Storage is a service for storing objects in Google Cloud. An object is an immutable piece of data consisting of a file of any format.
{: shortdesc}

 If you select **Google Cloud Storage** from the **Storage** section, configure the following details:

 | Field | Description |
 |--------------------------|----------------|
 | Display name | Enter the name to be displayed.|
 | Bucket name | Enter the bucket name.|
 | Endpoint | The default endpoint is selected.|
 | Upload JSON key file (.json) | Upload the JSON key file. |
 | Connection Status| Click the Test connection link to test the bucket connection. If the bucket connection is successful, a success message appears.|
 | Associate Catalog | Enable the toggle switch to add a catalog for your storage. This catalog is associated with your storage and serves as your query interface with the data stored within. |
 | Catalog type | Select the catalog type from the list. The supported catalogs are Apache Iceberg and Apache Hive. |
 | Catalog name | Enter the name of your catalog.|
 | Base path (optional) <br> **Note:** /n This field is available only in the watsonx.data Lite instance. /n This field appears only when you select Apache Iceberg as the catalog type. | Enter the base path for the catalog in the object storage. This allows you to associate multiple Iceberg catalogs with a single storage. <br>**Note:** You cannot share a storage between Iceberg and non-Iceberg catalogs. |
 | Associate | Click Associate to create the storage. |
 {: caption="Register bucket" caption-side="bottom"}

 For Google Cloud Storage, multiple buckets of different service accounts cannot be configured.
{: note}

If Google Cloud Storage is already inactive in old instances, the system will display the `Activate` button. Once you activate Google Cloud Storage, the system will automatically remove the `Activate` button.
{: note}
