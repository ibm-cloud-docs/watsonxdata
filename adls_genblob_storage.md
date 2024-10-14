---

copyright:
  years: 2022, 2024
lastupdated: "2024-10-10"

keywords: lakehouse, storage, catalog, watsonx.data

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

# Azure Data Lake Storage
{: #adls_genblob_storage}

Azure Data Lake Storage (ADLS) is a scalable data storage and analytics service that is hosted in Azure, Microsoft's public cloud. The Microsoft Azure Data Lake Storage connection supports access to both Gen1 and Gen2 Azure Data Lake Storage repositories.
{: shortdesc}

Select **Azure Data Lake Storage** from the **Storage** section of **Add component** window.

If you select **Azure Data Lake Storage Gen1 Blob** from the **Type** drop-down, configure the following details:

 | Field | Description |
 |--------------------------|----------------|
 | Display name | Enter the name to be displayed.|
 | Container name | Enter the container name. |
 | Storage account name | Enter the Storage account name. |
 | Endpoint | The Endpoint URL is auto-generated. |
 | Access key | Enter your access key. |
 | Associate catalog | Add a catalog for your storage. This catalog is associated with your storage and serves as your query interface with the data stored within. |
 | Activate now| Select the checkbox to activate the storage immediately or activate it later. |
 | Catalog type | Select the catalog type from the list. The recommended catalog is Apache Iceberg. The other options for catalog are Apache Hive, Apache Hudi, and Delta Lake. |
 | Catalog name | Enter the name of your catalog. |
 | Create | Click Create to create the storage. |
 {: caption="Register storage" caption-side="bottom"}

 If you select **Azure Data Lake Storage Gen2** from the **Type** drop-down, configure the following details:

 | Field | Description |
 |--------------------------|----------------|
 | Display name | Enter the name to be displayed.|
 | Container name | Enter the container name. |
 | Storage account name | Enter the Storage account name. |
 | Endpoint | The Endpoint URL is auto-generated. |
 | Application id | Enter the Application id. |
 | Directory id | Enter the directory id.    |
 | Secret key | Enter the secret key.  |
 | Associate catalog | Add a catalog for your storage. This catalog is associated with your storage and serves as your query interface with the data stored within. |
 | Activate now| Select the checkbox to activate the storage immediately or activate it later. |
 | Catalog type | Select the catalog type from the list. The recommended catalog is Apache Iceberg. The other options for catalog are Apache Hive, Apache Hudi, and Delta Lake. |
 | Catalog name | Enter the name of your catalog. |
 | Create | Click Create to create the storage. |
 {: caption="Register storage" caption-side="bottom"}
