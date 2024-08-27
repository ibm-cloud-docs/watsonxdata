---

copyright:
  years: 2022, 2024
lastupdated: "2024-08-22"

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

# Azure Data Lake Storage Gen1 Blob
{: #adls_genblob_storage}

Azure Data Lake Storage (ADLS) is a scalable data storage and analytics service that is hosted in Azure, Microsoft's public cloud. The Microsoft Azure Data Lake Storage connection supports access to both Gen1 and Gen2 Azure Data Lake Storage repositories.
{: shortdesc}

If you select **Azure Data Lake Storage Gen1 Blob** from the **Storage** section, configure the following details:

 | Field | Description |
 |--------------------------|----------------|
 | Display name | Enter the name to be displayed.|
 | Container name | Enter the container name. |
 | Storage account name | Enter the Storage account name. |
 | Endpoint | Enter the Endpoint URL. |
 | Authentication mode | Select the Authentication mode. \n * SAS: Enter your SAS token. \n * Account key: Enter your access key. |
 | Associate catalog | Add a catalog for your storage. This catalog is associated with your storage and serves as your query interface with the data stored within. |
 | Activate now| Activate the storage immediately or activate it later. |
 | Catalog type | Select the catalog type from the list. The recommended catalog is Apache Iceberg. The other options for catalog are Apache Hive, Apache Hudi, and Delta Lake. |
 | Catalog name | Enter the name of your catalog. |
 | Create | Click Create to create the storage. |
 {: caption="Table 1. Register storage" caption-side="bottom"}

 Azure Data Lake Storage Gen2 and Azure Data Lake Storage Gen1 Blob storage do not support SAS authentication mode for Presto (Java) engine.
 {: note}
