---

copyright:
  years: 2022, 2024
lastupdated: "2024-07-03"

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

This is a collection of frequently asked questions (FAQs) about the {{site.data.keyword.lakehouse_full}} service.
{: shortdesc}


## General  
{: #general}
{: faq}
{: support}

**What is IBM® {{site.data.keyword.lakehouse_short}}?**

IBM® {{site.data.keyword.lakehouse_short}} is an open, hybrid, and governed fit-for-purpose data store optimized to scale all data, analytics, and AI workloads to get greater value from your analytics ecosystem. It is a data management solution for collecting, storing, querying, and analyzing all your enterprise data (structured, semi-structured, and unstructured) with a single unified data platform. It provides a flexible and reliable platform that is optimized to work on open data formats.


**What can I do with IBM® {{site.data.keyword.lakehouse_short}}?**

You can use IBM® {{site.data.keyword.lakehouse_short}} to collect, store, query, and analyze all your enterprise data with a single unified data platform. You can connect to data in multiple locations and get started in minutes with built-in governance, security, and automation. You can use multiple query engines to run analytics, and AI workloads, reducing your data warehouse costs by up to 50%.

**Which data formats are supported in IBM® {{site.data.keyword.lakehouse_short}}?**

The following data formats are supported in IBM® {{site.data.keyword.lakehouse_short}}:
1. Ingestion: Data ingestion in IBM® {{site.data.keyword.lakehouse_short}} supports CSV and Parquet data file formats.
2. Create table from file: Create table from file in IBM® {{site.data.keyword.lakehouse_short}} supports CSV, Parquet, JSON, and TXT data file formats.

**What are the key features of IBM {{site.data.keyword.lakehouse_short}}?**

The key features of IBM® {{site.data.keyword.lakehouse_short}} are:
* An architecture that fully separates compute, metadata, and storage to offer ultimate flexibility.
* Multiple engines such as Presto (Java), Presto (C++), and Spark that provide fast, reliable, and efficient processing of big data at scale.
* Open formats for analytic data sets, allowing different engines to access and share the data at the same time.
* Data sharing between watsonx.data, Db2® Warehouse, and Netezza Performance Server or any other data management solution through common Iceberg table format support, connectors, and a shareable metadata store.
* Built-in governance that is compatible with existing solutions, including IBM Knowledge Catalog.
* Cost-effective, simple object storage is available across hybrid-cloud and multicloud environments.
* Integration with a robust ecosystem of IBM’s best-in-class solutions and third-party services to enable easy development and deployment of key use cases.

**What is the maximum size of the default IBM managed bucket?**

The IBM-managed bucket is a default 10 GB bucket.

## Presto (Java)
{: #presto}
{: faq}
{: support}

 **What is Presto (Java)?**

Presto (Java) is a distributed SQL query engine, with the capability to query vast data sets located in different data sources, thus solving data problems at scale.

**What are the Presto (Java) server types?**

A Presto (Java) installation includes three server types: coordinator, worker, and resource manager.

**What SQL statements are supported in IBM {{site.data.keyword.lakehouse_short}}?**

For information on supported SQL statements, see [Supported SQL statements](watsonxdata?topic=watsonxdata-supported_sql_statements).


## Metastore
{: #metastore}
{: faq}
{: support}

**What is HMS (Hive Metastore)?**

Hive Metastore (HMS) is a service that stores metadata that is related to Presto (Java) and other services in a backend Relational Database Management System (RDBMS) or Hadoop Distributed File System (HDFS).

## Installation and setup
{: #install}
{: faq}
{: support}


**How can I provision an IBM® {{site.data.keyword.lakehouse_short}} service instance?**

To provision an instance, see [Getting started with watsonx.data](watsonxdata?topic=watsonxdata-getting-started).

**How can I delete my IBM® {{site.data.keyword.lakehouse_short}} instance?**

To delete an instance, see [Deleting watsonx.data instance](watsonxdata?topic=watsonxdata-delete_lh).

**How can I access the IBM® {{site.data.keyword.lakehouse_short}} web console?**

To access the IBM® {{site.data.keyword.lakehouse_short}} web console, login to your IBM Cloud account and follow the steps as mentioned here [Open the web console](watsonxdata?topic=watsonxdata-getting-started) in [Getting started with watsonx.data](watsonxdata?topic=watsonxdata-getting-started).

**How can I provision an engine?**

From the IBM® {{site.data.keyword.lakehouse_short}} web console, go to Infrastructure manager to provision an engine. For more information, see [Provisioning an Engine](watsonxdata?topic=watsonxdata-prov_engine).

**How can I configure catalog or metastore?**

To configure a catalog with an engine, see [Associating a catalog with an engine](watsonxdata?topic=watsonxdata-asso-cat-eng).

**How can I configure a bucket?**

From the IBM® {{site.data.keyword.lakehouse_short}} web console, go to Infrastructure manager to configure a bucket. For more information, see [Adding a bucket-catalog pair](watsonxdata?topic=watsonxdata-reg_bucket).

## Access
{: #access}
{: faq}
{: support}

**How can I manage IAM access for IBM® {{site.data.keyword.lakehouse_short}}?**

{{site.data.keyword.Bluemix}} Identity and Access Management (IAM) controls access to IBM® {{site.data.keyword.lakehouse_short}} service instances for users in your account. Every user that accesses the IBM® {{site.data.keyword.lakehouse_short}} service in your account must be assigned an access policy with an IAM role. For more information, see [Managing IAM access for watsonx.data](watsonxdata?topic=watsonxdata-iam).

**How can I add and remove the users?**

To add or remove users in a component, see [Managing user access](watsonxdata?topic=watsonxdata-manage_access).

**How is the access control for users provided?**

To provide access control for users to restrict unauthorized access, see [Managing data policy rules](watsonxdata?topic=watsonxdata-data_policy).

**What is the process to assign access to a user?**

To assign access to a user, see [Managing roles and privileges](watsonxdata?topic=watsonxdata-role_priv).

**What is the process to assign access to a group?**

To assign access to a group, see [Managing roles and privileges](watsonxdata?topic=watsonxdata-role_priv).

## Presto (Java) Engine
{: #presto_engine}
{: faq}
{: support}

**How can I create an engine?**

To create an engine, see [Provisioning an Engine](watsonxdata?topic=watsonxdata-prov_engine).

**How can I pause and resume an engine?**

To pause an engine, see [Pause an Engine](watsonxdata?topic=watsonxdata-pause_engine).

To resume a paused engine, see [Resume an Engine](watsonxdata?topic=watsonxdata-resume_engine).

**How can I delete an engine?**

To delete an engine, see [Deleting an engine](watsonxdata?topic=watsonxdata-delete_engine).

**How can I run SQL queries?**

You can use the Query workspace interface in IBM® {{site.data.keyword.lakehouse_short}} to run SQL queries and scripts against your data. For more information, see [Running SQL queries](watsonxdata?topic=watsonxdata-run_sql).


## Databases and Connectors
{: #databases}
{: faq}
{: support}

**How can I add a database?**

To add a database, see [Adding a database-catalog pair](watsonxdata?topic=watsonxdata-reg_database).

**How can I remove a database?**

To remove a database, see [Deleting a database-catalog pair](watsonxdata?topic=watsonxdata-delete_database).

**What data sources does IBM® {{site.data.keyword.lakehouse_short}} currently support?**

IBM® {{site.data.keyword.lakehouse_short}} currently supports the following data sources:

1. IBM Db2
2. IBM Netezza
3. Apache Kafka
4. MongoDB
5. MySQL
6. PostgreSQL
7. SQL Server
8. Custom
9. Teradata
10. SAP HANA
11. Elasticsearch
12. SingleStore
13. Snowflake
14. IBM Data Virtualization Manager for z/OS

**How can I load the data into the IBM® {{site.data.keyword.lakehouse_short}}?**

There are 3 ways to load the data into the IBM® {{site.data.keyword.lakehouse_short}}.
1. Web console: You can use the Ingestion jobs tab from the Data manager page to securely and easily load data into the IBM® {{site.data.keyword.lakehouse_short}} console. For more information, see [Ingesting data by using Spark](watsonxdata?topic=watsonxdata-ingest_spark_ui).
2. Command-Line Interface: You can load data into IBM® {{site.data.keyword.lakehouse_short}} through CLI. For more information, see [Loading or ingesting data through CLI](watsonxdata?topic=watsonxdata-load_ingest_data#load_ingest_datacli).
3. Creating tables: You can load or ingest local data files to create tables by using the Create table option. For more information, see [Creating tables](watsonxdata?topic=watsonxdata-create_table).

**How can I create tables?**

You can create table through the Data manager page by using the web console. For more information, see [Creating tables](watsonxdata?topic=watsonxdata-create_table).

**How can I create schema?**

You can create schema through the Data manager page by using the web console. For more information, see [Creating schema](watsonxdata?topic=watsonxdata-create_schema).

**How can I query the loaded data?**

You can use the Query workspace interface in IBM® {{site.data.keyword.lakehouse_short}} to run SQL queries and scripts against your data. For more information, see [Running SQL queries](watsonxdata?topic=watsonxdata-run_sql).

## Ingestion
{: #ingestion}
{: faq}
{: support}

**What are the storage bucket options available?**

The storage bucket options available are IBM Storage Ceph, IBM Cloud Object Storage (COS), AWS S3, and MinIO object storage.

**What type of data files can be ingested?**

Only Parquet and CSV data files can be ingested.

**Can a folder of multiple files be ingested together?**

Yes a folder of multiple data files be ingested. A S3 folder must be created with data files in it for ingesting. The source folder must contain either all parquet files or all CSV files. For detailed information on S3 folder creation, see [Preparing for ingesting data](watsonxdata?topic=watsonxdata-prepare_ingest_data).

**What commands are supported in the command-line interface during ingestion?**

For commands supported in the command-line interface during ingestion, see [Loading or ingesting data through CLI](watsonxdata?topic=watsonxdata-load_ingest_data#load_ingest_datacli).


## Pricing plans
{: #pricing}
{: faq}

**Where can I learn more about each pricing plan?**

{{site.data.keyword.lakehouse_short}} as a service offers three pricing plans:
1. Lite plan: It provides a free usage limit of 2000 Resource Units (monitored on the Billing and usage page of IBM Cloud) within a time frame of 30 days. The cap value is displayed on the IBM Cloud catalog provisioning page and is reflected on your billing page within your {{site.data.keyword.lakehouse_short}} instance upon provisioning.
2. Enterprise plan: You pay by hour for each infrastructure resource that you add. Start with support services then build the engines and services that you want. This has an hourly rate that is computed in Resource Units that maps to your payment method whether ‘Pay as You Go’ or ‘Subscription’.
3. Enterprise BYOL plan: With the Enterprise BYOL plan, you have everything that is included in the Enterprise plan. If you have already purchased an on-premises {{site.data.keyword.lakehouse_short}} self-managed environment (paid per VPC) perpetual or subscription license, you can choose to use the license to apply for a discount on your SaaS Enterprise usage.

For more information, see [Pricing plans](watsonxdata?topic=watsonxdata-pricing-plans-1).

## Lite plan
{: #lite}
{: faq}

**Is the lite plan credit card free?**

Yes, if you use an IBM cloud trial account the lite plan is credit card free. You have a set amount of free usage limit of 2000 Resource Units within a time frame of 30 days, whichever ends first to try the product. For more information, see [Pricing plans](watsonxdata?topic=watsonxdata-pricing-plans-1).

**What's included in the lite plan?**

The lite plan is provided for you to try the basic features of watsonx.data and is available to all IBM Cloud account types like trial, pay-as-you-go, and subscription. It supports the basic features only. It is not available on AWS and is limited to one watsonx.data instance per IBM Cloud account (cross-regional).

Key supported features:
1. Ability to pause and resume Presto (Java) engine.
2. Ability to connect to an IBM Cloud-provided Cloud Object Storage (COS) bucket and provide credentials to your own COS or S3 bucket.
3. Ability to delete Presto (Java), Milvus, and connections to your own bucket.

Limitations:
1. It is limited to provisioning a single instance per resource group.
2. It is limited to 2000 resource units (RUs) before the instance is suspended. The cap value is displayed on the [{{site.data.keyword.Bluemix_notm}} catalog provisioning][def] page and is reflected on your billing page within your {{site.data.keyword.lakehouse_short}} instance upon provisioning. Your license expires on reaching either the cap limit of 2000 RUs or exceeding the trial period of 30 days.
3. It is limited to a maximum of one Presto (Java) engine or Milvus service with starter size (1.25 RUs per hour) or both.
4. It is limited to the smallest node sizes and profiles for each engine and service. You cannot increase the node size.
5. The lite instances cannot be used for production purposes.
6. The lite instances might be removed any time and are unrecoverable (no BCDR).
7. Engine scaling functions are not available.

**What is the limit for using the lite plan?**

The lite plan of {{site.data.keyword.lakehouse_short}} instance is typically a trial account that is free to use, with limits on capacity (2000 Resource Units), features for a time frame of 30 days. You can use the account to explore and familiarize yourself with watsonx.data. You need to create a paid IBM cloud account (either 'Pay as you go' or 'Subscription') and then provision an enterprise plan instance to access all the features and functions.

**I have exhausted all my resource units. How do I delete my lite plan instance?**

You can delete the lite plan instance from the resource group or IBM cloud resource collection will remove it after a period of 40 days.

**The lite plan has ended. How do I upgrade to the enterprise plan?**

Either before or after your lite plan has concluded, you can create a paid account whether 'Subscription' or 'Pay as you go' IBM Cloud. Now, you can create your new {{site.data.keyword.lakehouse_short}} instance. The enterprise plan is available on IBM Cloud and AWS environments.
You may create an enterprise plan instance once you have created a paid IBM cloud account (either 'Subscription' or 'Pay as you go') and then you can use a Cloud Object Store bucket that you own to store data.
For more information, see [How to create instance for {{site.data.keyword.lakehouse_short}} enterprise plan](watsonxdata?topic=watsonxdata-getting-started) and see [How to use a Cloud Object Store bucket that you own to store data](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-quick_start).

**How do I save data from a lite plan to an enterprise plan?**

You may create an IBM Cloud Object Store (COS) bucket that you own and connect it to your lite plan instance of {{site.data.keyword.lakehouse_short}}. You can then write data to that COS bucket that you own. Then, once you have created a paid IBM cloud account (either 'Pay as you go' or 'Subscription'), you can create an enterprise instance of {{site.data.keyword.lakehouse_short}} and connect it to the same COS bucket that you own to keep working with the same data files.

## Enterprise plan
{: #enterprise}
{: faq}

**What is included in the enterprise plan?**

In addition to the lite plan, the enterprise plan includes the following features:
1. You pay by hour for each infrastructure resource that you add. Starting with support services then build the engines and services that you want. This has an hourly rate that is computed in Resource Units that maps to your payment method whether ‘Pay as You Go’ or ‘Subscription’.
2. Presto (Java) and external Spark engine and Milvus service.
3. Hive metastore and Iceberg catalog.
4. Infrastructure manager and query editor.
5. Db2 Warehouse and Netezza integration.
6. Ability to scale (increase and decrease) node sizes for Presto (Java) engines.
7. Available on both IBM Cloud and AWS environments.

**What are the different payment plans under the enterprise plan?**

The different payment plans under the enterprise plan are ‘Subscription’ or ‘Pay as you go’.

**Is the cost for services like Milvus included in the enterprise plan?**

Yes, Milvus service is included in the enterprise plan.

## Bring Your Own License (modifications to pricing from enterprise plan)
{: #byol}
{: faq}

**How does Bring Your Own License work?**

With the Enterprise BYOL plan, you have everything that is included in the [Enterprise plan](watsonxdata?topic=watsonxdata-pricing-plans-1#enterprise-plan). If you have already purchased an on-premises {{site.data.keyword.lakehouse_short}} self-managed environment (paid per VPC) perpetual or subscription license, you can choose to use the license to apply for a discount on your SaaS Enterprise usage. For more information, see [BYOL Enterprise plan](watsonxdata?topic=watsonxdata-tutorial_prov_byol).

You cannot use both the VPCs in your own environment and on SaaS.
{: note}

**What platforms is it currently available on?**

Bring Your Own License is available only on the IBM Cloud platform now.

**What entitlements can I use for Bring Your Own License?**

The following are two parts that are eligible for a discount:
1. 5900-AYS perpetual license
2. 5900-AXD subscription software license

[def]: https://cloud.ibm.com/watsonxdata
