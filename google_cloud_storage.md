---

copyright:
  years: 2022, 2024
lastupdated: "2024-08-01"

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
 | Associate Catalog | Select the checkbox to add a catalog for your storage. This catalog is associated with your storage and serves as your query interface with the data stored within. |
 | Activate now| Activate the storage immediately or activate it later. |
 | Catalog type | Select the catalog type from the list. The supported catalogs are Apache Iceberg and Apache Hive. |
 | Catalog name | Enter the name of your catalog.|
 | Create | Click Create to create the storage. |
 {: caption="Register bucket" caption-side="bottom"}

 For Google Cloud Storage, multiple buckets of different service accounts cannot be configured.
{: note}
