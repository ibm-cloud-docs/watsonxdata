---

copyright:
  years: 2023, 2024
lastupdated: "2024-02-28"

keywords: watsonxdata, release notes

subcollection: watsonxdata

content-type: release-note

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

# Release notes for {{site.data.keyword.lakehouse_short}}
{: #release}

Use these release notes to learn about the latest updates to {{site.data.keyword.lakehouse_full}} that are grouped by date.
{: shortdesc}


## 28 Feb 2024 - Version 1.1.2
{: #lakehouse_Feb282024}


A new version of {{site.data.keyword.lakehouse_short}} was released in February 2024.

This release includes the following features and updates:

**SSL connection for data sources**
{: #feb_01_2024}

You can now enable SSL connection for the following data sources by using the **Add database** user interface to secure and encrypt the database connection.  :

* Db2

* PostgreSQL

For more information, see [Adding a database](watsonxdata?topic=watsonxdata-reg_database).

<!-- Issue-https://github.ibm.com/lakehouse/tracker/issues/5494

Issue-https://github.ibm.com/lakehouse/tracker/issues/2467

Issue-https://github.ibm.com/lakehouse/tracker/issues/6107  removed DVM as per slack conversationa and git issue comment from SAAS-Shanavi-->

**Secure ingestion job history**
{: #feb_02_2024}

Now, users can view only their own ingestion job history. Administrators can view the ingestion job history for all users.

<!-- Issue- https://github.ibm.com/lakehouse/tracker/issues/6500 -->


**Use more SQL statements**
{: #feb_03_2024}

You can now use the following SQL statements in the Query workspace to build and run queries against your data:

   * Apache Iceberg data sources
        - CREATE VIEW
        - DROP VIEW
   * MongoDB data sources
        - DELETE

<!-- Issue- https://github.ibm.com/lakehouse/tracker/issues/4678

Issue- https://github.ibm.com/lakehouse/tracker/issues/5782 -->


**New data types BLOB and CLOB for Teradata data source**
{: #feb_04_2024}

New data types BLOB and CLOB are available for Teradata data source. You can use these data types only with SELECT statements in the Query workspace to build and run queries against your data.

<!-- Issue- https://github.ibm.com/lakehouse/tracker/issues/7966 -->


**Create a new table during data ingestion**
{: #feb_06_2024}

Previously, you had to have a target table in {{site.data.keyword.lakehouse_short}} for ingesting data. Now, you can create a new table directly from the source data file (available in parquet or CSV format) by using data ingestion from the **Data Manager**. You can create the table by using the following methods of ingestion:

* Ingesting data by using Iceberg copy loader.

* Ingesting data by using Spark.

<!-- Issue- https://github.ibm.com/lakehouse/tracker/issues/7714

https://github.ibm.com/lakehouse/tracker/issues/7665 -->


**Perform ALTER TABLE operations on a column**
{: #feb_07_2024}

With an Iceberg data source, you can now perform ALTER TABLE operations on a column for the following data type conversions:

* int to bigint

* float to double

* decimal (num1, dec_digits) to decimal (num2, dec_digits), where num2>num1.

<!-- Issue: https://github.ibm.com/lakehouse/tracker/issues/7360  -->

**Better query performance by using sorted files**
{: #feb_09_2024}

With an Apache Iceberg data source, you can generate sorted files, which reduce the query result latency and improve the performance of Presto. Data in the Iceberg table is sorted during the writing process within each file. 

You can configure the order to sort the data by using the `sorted_by` table property. When you create the table, specify an array of one or more columns involved in sorting. To disable the feature, set the session property `sorted_writing_enabled` to false. 

<!-- Issue : https://github.ibm.com/lakehouse/tracker/issues/5201  -->

## 31 Jan 2024 - Version 1.1.1
{: #lakehouse_Jan312024}


A new version of {{site.data.keyword.lakehouse_short}} was released in January 2024.

This release includes the following features and updates:

**IBM Data Virtualization Manager for z/OS® connector**
{: #wn_01_2024}

You can now use the new IBM Data Virtualization Manager for z/OS® connector to read and write IBM Z® without moving, replicating, or transforming the data. For more information, see [Connecting to an IBM Data Virtualization Manager (DVM) data source](https://www.ibm.com/docs/en/iis/11.7?topic=analyzer-connecting-data-virtualization-manager-dvm-data-source).

**Teradata connector is enabled for multiple `ALTER TABLE` statements**
{: #wn_03_2024}

Teradata connector now supports the `ALTER TABLE RENAME TO`, `ALTER TABLE DROP COLUMN`, and `ALTER TABLE RENAME COLUMN column_name TO new_column_name` statements.

**Support for time travel queries**
{: #wn_05_2024}

Iceberg connector for Presto now supports time travel queries.

**The property `format_version` now shows the current version**
{: #wn_06_2024}

The property `format_version` now shows the correct value (current version) when you create an Iceberg table.


## 29 Nov 2023 - Version 1.1.0
{: #lakehouse_Nov292023}

A new version of {{site.data.keyword.lakehouse_short}} was released in November 2023.

This release includes the following features and updates:

**Presto case-sensitive behavior**
{: #wn_00}

The Presto behavior is changed from case-insensitive to case-sensitive. Now you can provide the object names in the original case format as in the database. For more information, see [Case-sensitive search configuration with Presto](watsonxdata?topic=watsonxdata-ts_cs).

**Roll-back feature**
{: #wn_01}

You can use the Rollback feature to rollback or rollforward to any snapshots for Iceberg tables.

<!-- **Improved query performance with caching**
{: #wn_03}

You can use the following types of caching to improve Presto query performance:

- Metastore caching
- File list caching
- File metadata caching

For more information, see [Enhancing query performance through caching](https://www.ibm.com/docs/SSDZ38_1.1.x/wxd/admin/enhance_qry.html). {: external} -->

**Capture Data Definition Language (DDL) changes**
{: #wn_04}

You can now capture and track the DDL changes in {{site.data.keyword.lakehouse_short}} by using an event listener.
For more information, see [Capturing DDL changes](watsonxdata?topic=watsonxdata-dll_changes).

**Ingest data by using Spark**
{: #wn_05}

You can now use the IBM Analytics Engine that is powered by Apache Spark to run ingestion jobs in {{site.data.keyword.lakehouse_short}}.

For more information, see [Ingesting data by using Spark](watsonxdata?topic=watsonxdata-ingest_spark_ui).

**Integration with Db2 and Netezza Performance Server**
{: #wn_06}

You can now register Db2 or Netezza Performance Server engines in {{site.data.keyword.lakehouse_short}} console.

For more information, see [Registering an engine](watsonxdata?topic=watsonxdata-reg_engine).

**New connectors**
{: #wn_07}

You can now use connectors in {{site.data.keyword.lakehouse_short}} to establish connections to the following types of databases:

- Teradata
- Delta Lake
- Elasticsearch
- SingleStoreDB
- Snowflake

For more information, see [Adding a database](watsonxdata?topic=watsonxdata-reg_database).

**AWS EMR for Spark**
{: #wn_08}

You can now run Spark applications from Amazon Web Services Elastic MapReduce (AWS EMR) to achieve the {{site.data.keyword.lakehouse_short}} Spark use cases:

- Data ingestion
- Data querying
- Table maintenance

For more information, see [Using AWS EMR for Spark use case](watsonxdata?topic=watsonxdata-spark-emr).

## 7 July 2023 - Version 1.0.0
{: #lakehouse_july72023}

{{site.data.keyword.lakehouse_short}} is a new open architecture that combines the elements of the data warehouse and data lake models. The best-in-class features and optimizations available on the {{site.data.keyword.lakehouse_short}} make it an optimal choice for next generation data analytics and automation. In the first release ({{site.data.keyword.lakehouse_short}} 1.0.0), the following features are supported:

- Creating, scaling, pausing, resuming, and deleting the Presto query engine
- Associating and dissociating a catalog with an engine
- Exploring catalog objects
- Adding and deleting a database-catalog pair
- Updating database credentials
- Adding and deleting bucket-catalog pair
- Exploring bucket objects
- Loading data
- Exploring data
- Querying data
- Query history
