---

copyright:
  years: 2022, 2025
lastupdated: "2025-06-10"

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

# IBM Storage Ceph
{: #ceph_storage}

IBM Storage Ceph is a scalable, open, software-defined storage platform. It combines an enterprise-hardened version of the Ceph storage system, with a Ceph management platform, deployment utilities, and support services.
{: shortdesc}

If you select **IBM Storage Ceph** from the **Storage** section, configure the following details:

 | Field | Description |
 |--------------------------|----------------|
 | Display name | Enter the name to be displayed.|
 | Bucket name | Enter your existing object storage bucket name.|
 | Endpoint | Enter the endpoint URL.|
 | Access key | Enter your access key. |
 | Secret key | Enter your secret key. |
 | Connection Status | Click the Test connection link to test the storage connection. If the connection is successful, a success message appears.|
 | Designate this bucket as the ACL store | Select the checkbox to designate this bucket as the ACL store.|
 | Associate catalog | Select the checkbox to add a catalog for your storage. This catalog is automatically associated with your storage and serves as your query interface with the data stored within. |
 | Activate now| Activate the storage immediately or activate it later. |
 | Catalog type | Select the catalog type from the list. The recommended catalog is Apache Iceberg. The other options for catalog are Apache Hive, Apache Hudi and Delta Lake.|
 | Catalog name | Enter the name of your catalog.|
 | Associate | Click Associate to create the storage. |
 {: caption="Register bucket" caption-side="bottom"}
