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

# MinIO
{: #minio_storage}

MinIO is a high-performance, S3 compatible object store. It is built for large scale data lake and database workloads.
{: shortdesc}

 You can use GlusterFS as backend filesystem for MinIO. For more information, see [Setting up GlusterFS replicated storage with MinIO](/docs/watsonxdata?topic=watsonxdata-setting_glusterfs).
 {: note}

 If you select **MinIO** from the **Storage** section, configure the following details:

 | Field | Description |
 |--------------------------|----------------|
 | Display name | Enter the name to be displayed.|
 | Bucket name | Enter your existing object storage bucket name.|
 | Endpoint | Enter the endpoint URL.|
 | Access key | Enter your access key. |
 | Secret key | Enter your secret key. |
 | Connection Status | Click the Test connection link to test the storage connection. If the connection is successful, a success message appears.|
 | Designate this bucket as the ACL store | Use the toggle switch to designate this bucket as the ACL store. If you enable the toggle switch, \n An **Enable Access Control List (ACL)?** dialog appears, Click **Enable**. \n This feature applies to {{site.data.keyword.lakehouse_short}} Premium, for more information see [Governance through Access Controlled Lists (AC)](https://dataplatform.cloud.ibm.com/docs/content/wsj/wx-data/gov_acl.html?context=wxd&audience=wdp). If you enable the toggle switch, the Associate catalog option is selected by default, with the Apache Iceberg catalog preselected. You cannot choose a different catalog for ACLs. You can designate only one storage as the ACL store per instance. After a storage is designated, this option will no longer be visible or available.|
 | Associate Catalog | Enable the toggle switch to add a catalog for your storage. This catalog is associated with your storage and serves as your query interface with the data stored within. |
 | Catalog type | Select the catalog type from the list. The recommended catalog is Apache Iceberg. The other options for catalog are Apache Hive, Apache Hudi and Delta Lake.|
 | Catalog name | Enter the name of your catalog.|
 | Base path (optional) <br> **Note:** /n This field is available only in the watsonx.data Lite instance. /n This field appears only when you select Apache Iceberg as the catalog type. | Enter the base path for the catalog in the object storage. This allows you to associate multiple Iceberg catalogs with a single storage. <br>**Note:** You cannot share a storage between Iceberg and non-Iceberg catalogs. |
 | Associate | Click Associate to create the storage. |
 {: caption="Register bucket" caption-side="bottom"}

If MinIO is already inactive in old instances, the system will display the `Activate` button. Once you activate MinIO, the system will automatically remove the `Activate` button.
{: note}
