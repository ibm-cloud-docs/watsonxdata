---

copyright:
  years: 2022, 2024
lastupdated: "2024-02-28"

keywords: watsonxdata, faq

subcollection: watsonxdata

content-type: faq

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:support: data-reuse='support'}
{:faq: data-hd-content-type='faq'}
{:video: .video}

# FAQs
{: #faqs}

This is a collection of frequently asked questions (FAQ) about the {{site.data.keyword.lakehouse_full}} service.
{: shortdesc}


## General  
{: #general}
{: faq}
{: support}

**What is IBM {{site.data.keyword.lakehouse_short}}?**
{: #feb_01_2024}

{{site.data.keyword.lakehouse_short}} is an open, hybrid, and governed fit-for-purpose data store optimized to scale all data, analytics and AI workloads to get greater value from your analytics ecosystem. It is a data management solution for collecting, storing, querying, and analyzing all your enterprise data (structured, semi-structured, and unstructured) with a single unified data platform. It provides a flexible and reliable platform that is optimized to work on open data formats.


**What can I do with IBM {{site.data.keyword.lakehouse_short}}?**
{: #feb_03_2024}

You can use {{site.data.keyword.lakehouse_short}} to collect, store, query, and analyze all your enterprise data with a single unified data platform. You can connect to data in multiple locations and get started in minutes with built-in governance, security and automation. You can leverage multiple query engines to run analytics and AI workloads, reducing your data warehouse costs by up to 50%.

**Which data formats are supported in {{site.data.keyword.lakehouse_short}}?**
{: #feb_04_2024}

The following data formats are supported in watsonx.data:

Ingestion: Data ingestion in watsonx.data supports .CSV and .Parquet data file formats.

Create Table: Create table in watsonx.data supports CSV, Parquet, JSON, TXT data file formats.

**What are the key features of IBM {{site.data.keyword.lakehouse_short}}?**
{: #feb_05_2024}

The key features of watsonx.data are:

* An architecture that fully separates compute, metadata, and storage to offer ultimate flexibility.

* Multiple engines such as Presto and Spark that provide fast, reliable, and efficient processing of big data at scale.

* Open formats for analytic data sets, allowing different engines to access and share the data at the same time.

* Data sharing between watsonx.data, Db2® Warehouse, and Netezza Performance Server or any other data management solution through common Iceberg table format support, connectors, and a shareable metadata store.

* Built-in governance that is compatible with existing solutions, including IBM Knowledge Catalog.

* Cost-effective, simple object storage is available across hybrid-cloud and multicloud environments.

* Integration with a robust ecosystem of IBM’s best-in-class solutions and third-party services to enable easy development and deployment of key use cases.

**What is the maximum size of the default IBM managed bucket?**
{: #feb_06_2024}

The IBM-managed bucket is a default 10 GB bucket.

## Presto
{: #presto}
{: faq}
{: support}

 **What is Presto?**
{: #feb_07_2024}

Presto is a distributed SQL query engine, with the capability to query vast data sets located in different data sources, thus solving data problems at scale.

**What are the Presto server types?**
{: #feb_08_2024}

A Presto installation includes three server types: Coordinator, Worker, and Resource manager.

**What SQL statements are supported in {{site.data.keyword.lakehouse_short}}?**
{: #feb_09_2024}

For information on supported SQL statements, see


## Metastore
{: #metastore}
{: faq}
{: support}

**What is HMS (Hive Metastore)?**
{: #feb_10_2024}

Hive Metastore (HMS) is a service that stores metadata related to Presto and other services in a backend Relational Database Management System (RDBMS) or Hadoop Distributed File System (HDFS).

## Installation and Setup
{: #install}
{: faq}
{: support}

**What version of Cloud Pak for Data do I need to use the latest version of {{site.data.keyword.lakehouse_short}}?**
{: #feb_11_2024}

For version updates, see

**How can I provision an IBM {{site.data.keyword.lakehouse_short}} service instance?**
{: #feb_12_2024}

To provision an instance, see

**How can I delete my {{site.data.keyword.lakehouse_short}} instance?**
{: #feb_13_2024}

To delete an instance, see [Deleting watsonx.data instance](watsonxdata?topic=watsonxdata-delete_lh)

**How can I access the IBM {{site.data.keyword.lakehouse_short}} web console?**
{: #feb_14_2024}

To access the IBM {{site.data.keyword.lakehouse_short}} web console web console, login to your IBM Cloud account and follow the steps as mentioned here [Open the web console](watsonxdata?topic=watsonxdata-getting-started) in [Getting started with watsonx.data](watsonxdata?topic=watsonxdata-getting-started).

**How can I configure an engine?**
{: #feb_15_2024}

From the watsonx.data web console, go to Infrastructure manager to configure an engine. For more information, see

**How can I configure catalog or metastore?**
{: #feb_16_2024}

To configure a catalog with an engine, see

**How can I configure a bucket?**
{: #feb_17_2024}

From the watsonx.data web console, go to Infrastructure manager to configure a bucket. For more information, see

## Access
{: #access}
{: faq}
{: support}

**How can I manage IAM access for {{site.data.keyword.lakehouse_short}}?**
{: #feb_18_2024}

{{site.data.keyword.Bluemix}} Identity and Access Management (IAM) controls access to {{site.data.keyword.lakehouse_short}} service instances for users in your account. Every user that accesses the watsonx.data service in your account must be assigned an access policy with an IAM role. For more information about IAM access for {{site.data.keyword.lakehouse_short}}, see [Managing IAM access for watsonx.data](watsonxdata?topic=watsonxdata-iam).


**How can I add and remove the users?**
{: #feb_19_2024}

To add or remove users in a component, see [Managing user access](watsonxdata?topic=watsonxdata-manage_access).


**How is the access control for users provided?**
{: #feb_20_2024}

To provide access control for users to restrict unauthorized access, see [Managing data policy rules](watsonxdata?topic=watsonxdata-data_policy).

**What is the process to assign access to a user?**
{: #feb_21_2024}

To assign access to a user, see

**What is the process to assign access to a group?**
{: #feb_22_2024}

To assign access to a group, see

## Presto Engine
{: #presto_engine}
{: faq}
{: support}

**How can I create an engine?**
{: #feb_23_2024}

To create an engine, see

**How can I pause and resume an engine?**
{: #feb_24_2024}

To pause an engine, use one of the following methods:

- Pausing an engine in list view

* Click the overflow menu icon at the end of the row and click Pause. A pause confirmation dialog appears.

* Click Pause.

- Pausing an engine in topology view

* Hover over the engine that you want to pause and click the Pause icon. A pause confirmation dialog appears.

* Click Pause.

To resume a paused engine, use one of the following methods:

- Resuming an engine in list view

* Click the overflow menu icon at the end of the row and click Resume.

- Resuming an engine in topology view

* Hover over the engine that you want to resume and click the Resume icon.

**How can I delete an engine?**
{: #feb_25_2024}

To delete an engine, see

**How can I run SQL queries?**
{: #feb_26_2024}

You can use the Query workspace interface in IBM® watsonx.data to run SQL queries and scripts against your data. For more information, see


## Databases and Connectors
{: #databases}
{: faq}
{: support}

**How can I add a database?**
{: #feb_27_2024}

To add a database, see

**How can I remove a database?**
{: #feb_28_2024}

To remove a database, see

**What data sources does watsonx.data currently support?**
{: #feb_29_2024}

Watsonx.data currently supports the following data sources:

·       IBM Db2

·       IBM Netezza

·       Apache Kafka

·       MongoDB

·       MySQL

·       PostgreSQL

·       SQL Server

·       Custom

·       Teradata

·       SAP HANA

·       Elasticsearch

·       SingleStore

·       Snowflake

·       IBM Data Virtualization Manager for z/OS

**How can I load the data into {{site.data.keyword.lakehouse_short}}?**
{: #feb_30_2024}

There are 3 ways to load the data into watsonx.data .

Web console: You can use the Ingestion jobs tab from the Data manager page to securely and easily load data into watsonx.data console. For more information, see

CLI: You can load data into watsonx.data either through CLI. For more information, see

Creating tables: You can also load or ingest local data files to create tables using the Create table option. For more information,

**How can I import data from a file?**
{: #feb_31_2024}

There are 3 ways to load the data into watsonx.data .

Web console: You can use the Ingestion jobs tab from the Data manager page to securely and easily load data into watsonx.data console. For more information, see

CLI: You can load data into watsonx.data either through CLI. For more information, see

Creating tables: You can also load or ingest local data files to create tables using the Create table option. For more information,

**How can I create tables?**
{: #feb_32_2024}

You can create table through Data manager page by using the web console. For more information, see

**How can I create schema?**
{: #feb_33_2024}

You can create schema through Data manager page by using the web console. For more information, see

**How can I query the loaded data?**
{: #feb_34_2024}

You can use the Query workspace interface in IBM® watsonx.data to run SQL queries and scripts against your data. For more information, see

## Ingestion
{: #ingestion}
{: faq}
{: support}

**What are the storage bucket options available?**
{: #feb_35_2024}

The storage bucket options available are IBM Storage Ceph, IBM Cloud Object Storage (COS), AWS S3, and MinIO object storage.

**What type of data files can be ingested?**
{: #feb_36_2024}

Only Parquet and CSV data files can be ingested.

**Can a folder of multiple files be ingested together?**
{: #feb_37_2024}

Yes a folder of multiple data files be ingested. S3 folder must be created with data files in it for ingesting. The source folder must contain either all parquet file or all CSV files. For detailed information on S3 folder creation, see

**What commands are supported in command line interface during ingestion?**
{: #feb_38_2024}

For commands supported in command line interface during ingestion, see

**What are the different options in watsonx.data to ingest or import files?**
{: #feb_39_2024}

There are 3 ways to load the data into watsonx.data .

Web console: You can use the Ingestion jobs tab from the Data manager page to securely and easily load data into watsonx.data console. For more information, see

CLI: You can load data into watsonx.data either through CLI. For more information, see

Creating tables: You can also load or ingest local data files to create tables using the Create table option. For more information, see
