---

copyright:
  years: 2023, 2024
lastupdated: "2024-04-03"

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

## 27 Mar 2024 - Version 1.1.3
{: #lakehouse_Mar272024}


A new version of {{site.data.keyword.lakehouse_short}} was released in March 2024.

This release includes the following features and updates:

**New data type for some data sources**
{: #mar_01_2024}

You can now use the BINARY data type  with the SELECT statement in the Query workspace to build and run queries against your data for the following data sources:

* Elasticsearch
* SQL Server
* MySQL

New data types: BLOB and CLOB are available for MySQL, PostgreSQL, Snowflake, SQL Server, and Db2 data sources. You can use these data types only with SELECT statements in the Query workspace to build and run queries against your data.

<!-- Issue-New DataType : Binary - #8397 , New DataType : BLOB & CLOB : [Release-2] - #8398 -->

**Delete data by using the DELETE FROM feature for Iceberg data sources**
{: #mar_02_2024}

You can now delete data from tables in Iceberg data sources by using the DELETE FROM feature.

You can specify the table property delete mode for new tables by using either copy-on-write mode or merge-on-read mode (default). For more information, see [SQL statements](watsonxdata?topic=watsonxdata-supported_sql_statements).

<!-- Support deleting whole partitions in Iceberg table - #8753

Support DELETEs on Iceberg tables via presto - #1563. - parent of 7767 and 7768

#7768#7767 -->

**ALTER VIEW statement for Iceberg data source**
{: #mar_03_2024}

You can now use the following SQL statement in the Query workspace to build and run queries against your data for ALTER VIEW:

ALTER VIEW name RENAME TO new_name

<!-- Support ALTER RENAME view in iceberg - #7610  -->

**Upload SSL certificates for Netezza Performance Server data sources**
{: #mar_03_2024}

You can now browse and upload the SSL certificate for SSL connections in Netezza Performance Server data sources. The valid file formats for SSL certificate are .pem, .crt, and .cer. You can upload SSL certificates by using the Adding a database-catalog pair option in the Infrastructure manager.

<!-- Enable Netezza connector for SSL connections - #7965   -->

**Query data from Db2 and Watson Query**
{: #mar_04_2024}

You can now query nicknames that are created in Db2 and virtualized tables from  Watson Query instances.
<!-- Support more table types in Db2 connector - #4724    -->


**SSL connection for IBM Data Virtualization Manager for z/OS data source**
{: #mar_05_2024}

You can now enable SSL connection for the IBM Data Virtualization Manager for z/OS data source by using the Add database user interface to secure and encrypt the database connection. Select Validate certificate to validate whether the SSL certificate that is returned by the host is trusted. You can choose to provide the hostname in the SSL certificate.

<!-- https://github.ibm.com/lakehouse/tracker/issues/6107    -->

**Use data from Apache Hudi catalog**
{: #mar_05_2024}

You can now connect to and use data from Apache Hudi catalog.

<!-- https://github.ibm.com/lakehouse/tracker/issues/8804

https://github.ibm.com/lakehouse/tracker/issues/9008    -->

**Add Milvus as a service in {{site.data.keyword.lakehouse_short}}**
{: #mar_06_2024}

You can now provision Milvus as a service in {{site.data.keyword.lakehouse_short}} with the following features:

* Provision different storage variants such as starter, medium, and large nodes.

* Assign Admin or User roles for Milvus users: User access policy is now available for Milvus users. Using the Access Control UI, you can assign Admin or User roles for Milvus users and also grant, revoke, or update the privilege. 

* Configure the Object storage for Milvus to store data. You can add or configure a custom bucket and specify the username, password, region, and bucket URL.

For more information, see [Milvus](watsonxdata?topic=watsonxdata-adding-milvus-service).
<!-- https://github.ibm.com/lakehouse/tracker/issues/7569
https://github.ibm.com/lakehouse/tracker/issues/7772

    -->

**Load data in batch by using the ibm-lh ingestion tool**
{: #mar_07_2024}

You can now use the ibm-lh ingestion tool to run batch ingestion procedures in non-interactive mode (from outside the ibm-lh-tools container), by using the ibm-lh-client package. For more information, see [ibm-lh commands and usage](https://www.ibm.com/docs/SSDZ38_1.1.x/wxd-client/topics/ibm_lh_commands.html).

 <!-- https://github.ibm.com/lakehouse/tracker/issues/9132     -->

**Creating schema by using bulk ingestion in web console**
{: #mar_08_2024}

You can now create a schema by using the bulk ingestion process in the web console, if the schema is not previously created.

<!-- https://github.ibm.com/lakehouse/tracker/issues/8885     -->

**Use time-travel queries in Apache Iceberg tables**
{: #mar_09_2024}

You can now run the following time-travel queries by using branches and tags in Apache Iceberg table snapshots:

- SELECT *FROM `<table name>` FOR VERSION AS OF 'historical-tag'

- SELECT *FROM `<table name>` FOR VERSION AS OF 'test-branch'

<!-- https://github.ibm.com/lakehouse/tracker/issues/7651     -->


**Access Cloud Object Storage without credentials**
You can now access your Cloud Object Storage bucket without credentials, by using the Content Aware Storage (CAS) endpoint. For more information about getting CAS endpoint, see [Getting CAS endpoint](watsonxdata?topic=watsonxdata-cas_ep).

<!-- https://github.ibm.com/lakehouse/tracker/issues/8993     -->


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


**SQL enhancements**
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
