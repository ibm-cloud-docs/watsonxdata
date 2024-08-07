---

copyright:
  years: 2022, 2024
lastupdated: "2024-08-02"

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

A storage is an existing, externally managed storage. It is one of the data sources for {{site.data.keyword.lakehouse_full}}. A catalog defines the schemas and metadata for a data source.
{: shortdesc}

When you add your own storage bucket or database, or query the data in these data sources through the query engines of {{site.data.keyword.lakehouse_short}}, egress charges for pulling data out of these sources might apply depending on your service provider. If you are using managed services, consult your service provider's documentation or support for details about these charges.
{: important}

To reduce the latency issues, it is recommended to colocate your additional storage buckets or databases in the region where {{site.data.keyword.lakehouse_short}} instance is provisioned.
{: important}


To add a storage-catalog pair, complete the following steps:

1. Log in to the {{site.data.keyword.lakehouse_short}} console.
2. From the navigation menu, select **Infrastructure manager**.
3. To define and connect a storage, click **Add component** and select **Add storage**.
4. In the **Add storage** window, select a storage from the storage type drop-down list and provide the required details to connect to existing externally managed storage.  Based on the storage type selected, click the respective link to configure the storage details.

* [IBM Cloud Object Storage](#cos)
* [IBM Storage Ceph](#ceph)
* [Amazon S3](#cos)
* [Hadoop Distributed File System (HDFS)](#hdfs)
* [MinIO](#ceph)
* [Google Cloud Storage](#gcs)
* [Azure Data Lake Storage Gen1 Blob](#genblob)
* [Azure Data Lake Storage Gen2](#gen)

   * **IBM Cloud Object Storage or Amazon S3**{: #cos}

       If you select **IBM Cloud Object Storage or Amazon S3** from the **Storage type** drop-down list, configure the following details:

      | Field | Description |
      |--------------------------|----------------|
      | Display name | Enter the name to be displayed.|
      | Bucket name | Enter your existing object storage bucket name.|
      | Region | Select the region where the storage is available.|
      | Endpoint | Enter the endpoint URL.|
      | Access key | Enter your access key. |
      | Secret key | Enter your secret key. |
      | Connection Status | Click the Test connection link to test the storage connection. If the connection is successful, a success message appears.|
      | Associate Catalog | Select the checkbox to add a catalog for your storage. This catalog is associated with your storage and serves as your query interface with the data stored within. |
      | Activate now| Activate the storage immediately or activate it later. |
      | Catalog type | Select the catalog type from the list. The recommended catalog is Apache Iceberg. The other options for catalog are Apache Hive, Apache Hudi, and Delta Lake.|
      | Catalog name | Enter the name of your catalog.|
      {: caption="Table 1. Register bucket" caption-side="bottom"}

   * **IBM Storage Ceph or MinIO**{: #ceph}

       If you select **IBM Storage Ceph or MinIO** from the **Storage type** drop-down list, configure the following details:

      | Field | Description |
      |--------------------------|----------------|
      | Display name | Enter the name to be displayed.|
      | Bucket name | Enter your existing object storage bucket name.|
      | Endpoint | Enter the endpoint URL.|
      | Access key | Enter your access key. |
      | Secret key | Enter your secret key. |
      | Connection Status | Click the Test connection link to test the storage connection. If the connection is successful, a success message appears.|
      | Associate catalog | Select the checkbox to add a catalog for your storage. This catalog is automatically associated with your storage and serves as your query interface with the data stored within. |
      | Activate now| Activate the storage immediately or activate it later. |
      | Catalog type | Select the catalog type from the list. The recommended catalog is Apache Iceberg. The other options for catalog are Apache Hive, Apache Hudi and Delta Lake.|
      | Catalog name | Enter the name of your catalog.|
      {: caption="Table 1. Register bucket" caption-side="bottom"}

   * **Hadoop Distributed File System (HDFS)**{: #hdfs}

       If you select **Hadoop Distributed File System (HDFS)** from the **Storage type** drop-down list, configure the following details:

      | Field | Description |
      |--------------------------|----------------|
      | Display name | Enter the name to be displayed.|
      | Thrift URI | Enter the Thrift URI.|
      | Thrift Port | Enter the Thrift port. |
      | Kerberos authentication | Select the checkbox **Kerberos authentication** for secure connection.  \n a. Enter the following information: \n i. HDFS principal \n ii. Hive client principal \n iii. Hive server principal \n b. Upload the following files: \n i. Kerberos config file (.config) \n ii. HDFS keytab file (.keytab) \n iii. Hive keytab file (.keytab) |
      | Upload core site file (.xml) | Upload core site file (.xml) |
      | Upload HDFS site file (.xml) | Upload HDFS site file (.xml) |
      | Associate catalog | Add a catalog for your storage. This catalog is associated with your storage and serves as your query interface with the data stored within. |
      | Catalog type | The supported catalog is Apache Hive.|
      | Catalog name | Enter the name of your catalog. |
      {: caption="Table 1. Register bucket" caption-side="bottom"}

   * **Google Cloud Storage**{: #gcs}

       If you select **Google Cloud Storage** from the **Storage type** drop-down list, configure the following details:

      | Field | Description |
      |--------------------------|----------------|
      | Display name | Enter the name to be displayed.|
      | Bucket name | Enter the bucket name.|
      | Upload JSON key file (.json) | Upload the JSON key file. |
      | Associate Catalog | Select the checkbox to add a catalog for your storage. This catalog is associated with your storage and serves as your query interface with the data stored within. |
      | Activate now| Activate the storage immediately or activate it later. |
      | Catalog type | Select the catalog type from the list. The supported catalogs are Apache Iceberg and Apache Hive. |
      | Catalog name | Enter the name of your catalog.|
      {: caption="Table 1. Register bucket" caption-side="bottom"}

     For Google Cloud Storage, multiple buckets of different service accounts cannot be configured.
    {: note}

   * **Azure Data Lake Storage Gen1 Blob**{: #genblob}

       If you select **Azure Data Lake Storage Gen1 Blob** from the **Storage type** drop-down list, configure the following details:

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
      {: caption="Table 1. Register bucket" caption-side="bottom"}

   * **Azure Data Lake Storage Gen2**{: #gen}

       If you select **Azure Data Lake Storage Gen2** from the **Storage type** drop-down list, configure the following details:

      | Field | Description |
      |--------------------------|----------------|
      | Display name | Enter the name to be displayed.|
      | Container name | Enter the container name. |
      | Storage account name | Enter the Storage account name. |
      | Endpoint | Enter the Endpoint URL. |
      | Authentication mode | Select the Authentication mode. \n * SAS: Enter your SAS token. \n * Service Principle: Enter the Application id, Directory id and Secret key. |
      | Associate catalog | Add a catalog for your storage. This catalog is associated with your storage and serves as your query interface with the data stored within. |
      | Activate now| Activate the storage immediately or activate it later. |
      | Catalog type | Select the catalog type from the list. The recommended catalog is Apache Iceberg. The other options for catalog are Apache Hive, Apache Hudi, and Delta Lake. |
      | Catalog name | Enter the name of your catalog. |
      {: caption="Table 1. Register bucket" caption-side="bottom"}

     Azure Data Lake Storage Gen2 and Azure Data Lake Storage Gen1 Blob storage do not support SAS authentication mode for Presto (Java) engine.
     {: note}

5. Click **Create**.

     You can modify the access key and secret key of a user-registered bucket for a storage. This feature is only available for user-registered buckets and is not applicable to default buckets, ADLS, or Google Cloud Storage. This feature can only be used if the new credentials successfully pass the test connection.
     {: note}

   **Important information**{: #important_info}
   * The storage bucket name must be unique and must contain only the characters A–Z, a–z, 0–9, and hypen (-).
   * You must use a service credential with `Writer` role because the schema is written to the storage bucket. Make sure that you choose the endpoint that matches the type of access that the bucket allows. That is, if no public access is allowed (**Public access** is **No**) to the bucket, choose the **Direct** endpoint.

## Features
{: #connector_features}

1. For **Iceberg** connector:
* You can delete data from tables by using `DELETE FROM` statement for **Iceberg** connector.
* You can specify the table property delete_mode for new tables by using either copy-on-write mode or merge-on-read mode (default).
2. For `DELETE FROM` statement for **Iceberg** connector:
* Filtered columns only support comparison operators, such as EQUALS, LESS THAN, or LESS THAN EQUALS.
* Deletes must only occur on the latest snapshot.
* For V1 tables, the **Iceberg** connector can delete data only in one or more entire partitions. Columns in the filter must all be identity-transformed partition columns of the target table.
3. For `CREATE TABLE`, **Iceberg** connector supports `sorted_by` table property.
* When you create the table, specify an array of one or more columns that are involved.
4. For **Iceberg** connector, `ALTER TABLE` operations on a column support data type conversions from:
* `INT` to `BIGINT`
* `FLOAT` to `DOUBLE`
* `DECIMAL` (num1, dec_digits) to `DECIMAL` (num2, dec_digits), where num2>num1.

## Limitations
{: #a_limitations}

* Use separate containers and storage accounts for ADLS Gen1 and ADLS Gen2 storage for complete metadata synchronization, including tables. Otherwise, a PARTIAL SUCCESS message appears in the sync logs when SYNC finishes.

## Limitations for SQL statements
{: #sql_limitations}

1. For **Iceberg**, **Memory** and **Hive** connectors, `DROP SCHEMA` can do `RESTRICT` by default.
2. For database-based catalogs the `CREATE SCHEMA`, `CREATE TABLE`, `DROP SCHEMA`, `DROP TABLE`, `DELETE`, `DROP VIEW`, `ALTER TABLE`, and `ALTER SCHEMA` statements are not available in the **Data Manager** UI.

## Limitations for data types
{: #datatypes_limitations}

1. For **Iceberg** connector, the maximum number of digits that can be accommodated in a column of data type FLOAT and DOUBLE is 37. Trying to insert anything larger ends up in a decimal overflow error.
2. When the fields of data type `REAL` have 6 digits or more in the decimal part with the digits being predominately zero, the values when queried are rounded off. It is observed that the rounding off occurs differently based on the precision of the values. For example, a decimal number 1.654 when rounded to 3-digits after decimal point are the same. Another example, is 10.890009 and 10.89000. It is noticed that 10.89000 is rounded to 10.89, whereas 10.89009 is not rounded off. This is an inherent issue because of the representational limitations of binary floating point formats. This might have a significant impact when querying involves sorting.

For more information on mixed-case feature flag behavior, supported SQL statements and supported data types matrices, see [Support content](https://www.ibm.com/support/pages/node/7157339){: external}.
