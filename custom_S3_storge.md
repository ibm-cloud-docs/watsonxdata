---

copyright:
  years: 2022, 2025
lastupdated: "2026-02-18"

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

# Custom S3 Storage
{: #custom_s3_storage}

If your S3 storage is already available under one of the predefined storage providers (for example, IBM COS, Ceph, or AWS S3), use the respective provider instead of the Custom S3 option.
{: important}

You can configure any S3 compatible object storage in {{site.data.keyword.lakehouse_short}} using the **Custom S3 Storage** option. This feature supports a wide range of third-party storage providers that implement the S3 API standard.
{: shortdesc}

IBM supports **NetApp** and **Oracle Cloud Infrastructure (OCI)**.
{: note}

If you select **Custom S3 Storage** from the **Storage** section, configure the following details:

 | Field | Description |
 | --- | --- |
 | Display name | Enter the name to be displayed. |
 | Bucket name | Enter the name of your existing bucket. |
 | Region | Enter the S3 storage region if required for access. If not, leave this field blank. |
 | Endpoint Type | Select the endpoint access type. Options are **Path style access** or **Virtual host**. <br><br>**Note:** Verify which access type your storage uses and select the appropriate option accordingly. |
 | Endpoint | Enter the **Endpoint** URL. Test connection is enabled when the endpoint is provided. The endpoint represents only the base service endpoint and must be provided in standard base URL format, regardless of whether you select **Path style access** or **Virtual host** in the Endpoint Type field. For example, `https://s3.us-east-1.amazonaws.com` or `https://s3.amazonaws.com`. You do not need to modify the endpoint format based on the bucket addressing style. <br><br>**Note:** For **OCI storage**, the endpoint must follow this format:<br>`https://<namespace>.compat.objectstorage.<region>.oraclecloud.com` |
 | Access key  | Enter your access key. |
 | Secret key  | Enter your secret key. |
 | Connection status | Click the **Test connection** link to test the bucket connection. If the bucket connection is successful, a success message appears. |
 | Associate catalog | Enable the toggle switch to add a catalog for your storage. This catalog is associated with your storage and serves as your query interface with the data stored within. || Catalog type | Select the catalog type from the list. The recommended catalog is Apache Iceberg. The other options for catalog are Apache Hive, Apache Hudi, and Delta Lake. |
 | Catalog name | Enter the name of the associated catalog. |
 | Base path (optional) <br> **Note:** This field is available only in the {{site.data.keyword.lakehouse_short}} Lite instance. This field appears only when you select Apache Iceberg as the catalog type.. | Enter the base path for the catalog in the object storage. This allows you to associate multiple Iceberg catalogs with a single storage. <br>**Note:** You cannot share a storage between Iceberg and non-Iceberg catalogs. |
 | Associate | Click **Associate** to create the storage. |
 {: caption="Custom S3 Storage" caption-side="bottom"}
