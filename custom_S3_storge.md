---

copyright:
  years: 2022, 2025
lastupdated: "2025-10-27"

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
 | Endpoint | Enter the **Endpoint** URL. Test connection is enabled when the endpoint is provided. |
 | Access key<br>Secret key | If you are using secrets from vault, then select the **Access key** and **Secret key** from the respective drop-down lists. Otherwise, enter your **Access key** and **Secret key** in the respective fields. |
 | Connection status | Click the **Test connection** link to test the bucket connection. If the bucket connection is successful, a success message appears. |
 | Associate catalog | Enable the toggle switch to add a catalog for your storage. This catalog is associated with your storage and serves as your query interface with the data stored within. || Catalog type | Select the catalog type from the list. The recommended catalog is Apache Iceberg. The other options for catalog are Apache Hive, Apache Hudi, and Delta Lake. |
 | Catalog name | Enter the name of the associated catalog. |
 | Associate | Click **Associate** to create the storage. |
