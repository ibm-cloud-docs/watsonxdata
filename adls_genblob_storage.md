---

copyright:
  years: 2022, 2025
lastupdated: "2025-12-02"

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


Azure Data Lake Storage (ADLS) Gen1 is deprecated and will be removed in an upcoming release. You must transition to ADLS Gen2 as ADLS Gen1 will no longer be available.
{: important}

If you select **Azure Data Lake Storage Gen1 Blob** from the **Type** drop-down, configure the following details:

 | Field | Description |
 |--------------------------|----------------|
 | Display name | Enter the name to be displayed.|
 | Container name | Enter the container name. |
 | Storage account name | Enter the Storage account name. |
 | Endpoint | The Endpoint URL is auto-generated. |
 | Access key | Enter your access key. |
 | Connection Status | Click the Test connection link to test the storage connection. If the connection is successful, a success message appears.|
 | Associate catalog | Enable the toggle switch to add a catalog for your storage. This catalog is associated with your storage and serves as your query interface with the data stored within.|
 | Catalog type | Select the catalog type from the list. The recommended catalog is Apache Iceberg. The other options for catalog are Apache Hive, Apache Hudi, and Delta Lake. |
 | Catalog name | Enter the name of your catalog. |
 | Base path (optional) <br> **Note:** /n This field is available only in the watsonx.data Lite instance. /n This field appears only when you select Apache Iceberg as the catalog type. | Enter the base path for the catalog in the object storage. This allows you to associate multiple Iceberg catalogs with a single storage. <br>**Note:** You cannot share a storage between Iceberg and non-Iceberg catalogs. |
 | Associate | Click Associate to create the storage. |
 {: caption="Register storage" caption-side="bottom"}

 If you select **Azure Data Lake Storage Gen2** from the **Type** drop-down, configure the following details:

 | Field | Description |
 |--------------------------|----------------|
 | Display name | Enter the name to be displayed.|
 | Container name | Enter the container name. |
 | Storage account name | Enter the Storage account name. |
 | Endpoint | The Endpoint URL is auto-generated. |
 | Authentication Mode     | Based on your requirement, select one of the following mode of authentication :\n i. Account Key: If you select Account Key, enter the access key in the Access Key field. \n ii. Service Principal: If you select Service Principal, enter the Application id, Directory id, and Secret key.|
 | Connection Status | Click the Test connection link to test the storage connection. If the connection is successful, a success message appears.|
 | Associate catalog | Enable the toggle switch to add a catalog for your storage. This catalog is associated with your storage and serves as your query interface with the data stored within.|
 | Catalog type | Select the catalog type from the list. The recommended catalog is Apache Iceberg. The other options for catalog are Apache Hive, Apache Hudi, and Delta Lake. |
 | Catalog name | Enter the name of your catalog. |
 | Base path (optional) <br> **Note:** /n This field is available only in the watsonx.data Lite instance. /n This field appears only when you select Apache Iceberg as the catalog type. | Enter the base path for the catalog in the object storage. This allows you to associate multiple Iceberg catalogs with a single storage. <br>**Note:** You cannot share a storage between Iceberg and non-Iceberg catalogs. |
 | Associate | Click Associate to create the storage. |
 {: caption="Register storage" caption-side="bottom"}

If ADLS is already inactive in old instances, the system will display the `Activate` button. Once you activate ADLS, the system will automatically remove the `Activate` button.
{: note}
