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

# Hadoop Distributed File System
{: #hdfs_storage}

Hadoop Distributed File System (HDFS) is a file system that manages large data sets that can run on commodity hardware.
{: shortdesc}

 If you select **Hadoop Distributed File System (HDFS)** from the **Storage** section, configure the following details:

 | Field | Description |
 |--------------------------|----------------|
 | Display name | Enter the name to be displayed.|
 | Thrift URI | Enter the Thrift URI.|
 |Thrift Port | Enter the Thrift port. |
 | Kerberos authentication | Select the checkbox **Kerberos authentication** for secure connection.  \n a. Enter the following information: \n i. HDFS principal \n ii. Hive client principal \n iii. Hive server principal \n b. Upload the following files: \n i. Kerberos config file (.config) \n ii. HDFS keytab file (.keytab) \n iii. Hive keytab file (.keytab) |
 | Upload core site file (.xml) | Upload core site file (.xml) |
 | Upload HDFS site file (.xml) | Upload HDFS site file (.xml) |
 | Associate catalog | Add a catalog for your storage. This catalog is associated with your storage and serves as your query interface with the data stored within. |
 | Catalog type | The supported catalog is Apache Hive.|
 | Catalog name | Enter the name of your catalog. |
 | Create | Click Create to create the storage. |
 {: caption="Register bucket" caption-side="bottom"}
