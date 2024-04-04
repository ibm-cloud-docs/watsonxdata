---

copyright:
  years: 2022, 2024
lastupdated: "2024-04-03"

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

# Adding a storage-catalog pair
{: #reg_bucket}

A storage is an existing, externally managed object storage. It is one of the data sources for {{site.data.keyword.lakehouse_full}}. A catalog defines the schemas and metadata for a data source.
{: shortdesc}

When you add your own object storage bucket or database, or query the data in these data sources through the query engines of {{site.data.keyword.lakehouse_short}}, egress charges for pulling data out of these sources might apply depending on your service provider. If you are using managed services, consult your service provider's documentation or support for details about these charges.
{: important}

To reduce the latency issues, it is recommended to colocate your additional object storage buckets or databases in the region where {{site.data.keyword.lakehouse_short}} instance is provisioned.
{: important}


To add a storage-catalog pair, complete the following steps.

1. Log in to the {{site.data.keyword.lakehouse_short}} console.
2. From the navigation menu, select **Infrastructure manager**.
3. To define and connect a storage, click **Add component** and select **Add storage**.
4. In the **Add storage** window, select a storage from the storage type drop-down list and provide the required details to connect to existing externally managed object storage. The list includes the following storage types:
    * IBM Cloud Object Storage
    * IBM Storage Ceph
    * Amazon S3
    * Hadoop Distributed File System (HDFS)
    * MinIO
5. Based on the storage type selected, click the respective link to configure the storage details.

    * [IBM Cloud Object Storage](#cos)
    * [IBM Storage Ceph](#ceph)
    * [Amazon S3](#cos)
    * [Hadoop Distributed File System (HDFS)](#hdfs)
    * [MinIO](#ceph)


 * **IBM Cloud Object Storage or Amazon S3**{: #cos}

    If you select **IBM Cloud Object Storage or Amazon S3** from the **Storage type** drop-down list, configure the following details:

   | Field | Description |
   |--------------------------|----------------|
   | Storage type | Select the storage type from the list.|
   | Region | Select the region where the storage is available.|
   | Bucket name | Enter your existing object storage bucket name.|
   | Display name | Enter the name to be displayed.|
   | Endpoint | Enter the endpoint URL.|
   | Access key | Enter your access key. |
   | Secret key | Enter your secret key. |
   | Connection Status | Click the Test connection link to test the storage connection. If the connection is successful, a success message appears.|
   | Associate Catalog | Select the checkbox to add a catalog for your storage. This catalog is associated with your storage and serves as your query interface with the data stored within. |
   | Activate now| Activate the storage immediately or activate it later. |
   | Catalog type | Select the catalog type from the list. The recommended catalog is Apache Iceberg. The other options for catalog are Apache Hive, Apache Hudi and Delta Lake.|
   | Catalog name | Enter the name of your catalog.|
   {: caption="Table 1. Register bucket" caption-side="bottom"}


 * **IBM Storage Ceph or MinIO**{: #ceph}

    If you select **IBM Storage Ceph or MinIO** from the **Storage type** drop-down list, configure the following details:

   | Field | Description |
   |--------------------------|----------------|
   | Storage type | Select the storage type from the list.|
   | Bucket name | Enter your existing object storage bucket name.|
   | Display name | Enter the name to be displayed.|
   | Endpoint | Enter the endpoint URL.|
   | Access key | Enter your access key. |
   | Secret key | Enter your secret key. |
   | Connection Status | Click the Test connection link to test the storage connection. If the connection is successful, a success message appears.|
   | Associate Catalog | Select the checkbox to add a catalog for your storage. This catalog is automatically associated with your storage and serves as your query interface with the data stored within. |
   | Activate now| Activate the storage immediately or activate it later. |
   | Catalog type | Select the catalog type from the list. The recommended catalog is Apache Iceberg. The other options for catalog are Apache Hive, Apache Hudi and Delta Lake.|
   | Catalog name | Enter the name of your catalog.|
   {: caption="Table 1. Register bucket" caption-side="bottom"}


    * **Hadoop Distributed File System (HDFS)**{: #hdfs}

    If you select **Hadoop Distributed File System (HDFS)* from the **Storage type** drop-down list, configure the following details:

   | Field | Description |
   |--------------------------|----------------|
   | Storage type | Select the storage type from the list.|
   | Display name | Enter the name to be displayed.|
   | Thrift URI | Enter the Thrift URI.|
   | Thrift Port | Enter the Thrift port. |
   | Upload core site file (.xml) | Upload core site file (.xml) |
   | Upload HDFS site file (.xml) | Upload HDFS site file (.xml) |
   | Associated Catalog | Add a catalog for your storage. This catalog is associated with your storage and serves as your query interface with the data stored within. |
   | Catalog type | The supported catalog is Apache Hive.|
   | Catalog name | Enter the name of your catalog. |
   {: caption="Table 1. Register bucket" caption-side="bottom"}

The object storage bucket name must be unique. You must use unique names while creating buckets in different object stores.
{: important}

5. Click **Add**.
