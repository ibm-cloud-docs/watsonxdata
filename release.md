---

copyright:
  years: 2023, 2023
lastupdated: "2023-11-29"

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

## 29 Nov 2023
{: #lakehouse_Nov292023}

## Version 1.1.0
{: #version_110}

A new version of {{site.data.keyword.lakehouse_short}} was released in November 2023.

This release includes the following features and updates:

**Time-travel and roll-back queries**
{: #wn_01}

You can now run the following time-travel queries to access historical data in Apache Iceberg tables:

```SQL
SELECT <columns> FROM <iceberg-table> FOR TIMESTAMP AS OF TIMESTAMP <timestamp>;
SELECT <columns> FROM <iceberg-table> FOR VERSION AS OF <snapshotId>;
```
{: codeblock}

You can use time-travel queries to query and restore data that was updated or deleted in the past.
You can also roll back an Apache Iceberg table to any existing snapshot.

**Capture historical data about Presto queries**
{: #wn_02}

The Query History Monitoring and Management (QHMM) service captures historical data about Presto queries and events. The historical data is stored in a MinIO bucket and you can use the data to understand the queries that were run and to debug the Presto engine.

For more information, see [Monitoring and managing diagnostic data](https://www.ibm.com/docs/SSDZ38_1.1.x/lh-console/topics/qhmm.html). {: external}

**Improved query performance with caching**
{: #wn_03}

You can use the following types of caching to improve Presto query performance:

- Metastore caching
- File list caching
- File metadata caching

For more information, see [Enhancing query performance through caching](https://www.ibm.com/docs/SSDZ38_1.1.x/wxd/admin/enhance_qry.html). {: external}

**Capture Data Definition Language (DDL) changes**
{: #wn_04}

You can now capture and track the DDL changes in {{site.data.keyword.lakehouse_short}} by using an event listener.
For more information, see [Capturing DDL changes](https://www.ibm.com/docs/SSDZ38_1.1.x/lh-console/topics/ddl_changes.html).

**Ingest data by using Spark**
{: #wn_05}

You can now use the IBM Analytics Engine powered by Apache Spark to run ingestion jobs in {{site.data.keyword.lakehouse_short}}.

For more information, see [Ingesting data by using Spark](https://www.ibm.com/docs/SSDZ38_1.1.x/lh-console/topics/ingestion_spark.html). {: external}

**Integration with Db2 and Netezza Performance Server**
{: #wn_06}

You can now register Db2 or Netezza Performance Server engines in {{site.data.keyword.lakehouse_short}} console.

For more information, see [Registering an engine](https://www.ibm.com/docs/SSDZ38_1.1.x/lh-console/topics/reg_engine.html). {: external}

**New connectors**
{: #wn_07}

You can now use connectors in {{site.data.keyword.lakehouse_short}} to establish connections to the following types of databases:

- Teradata
- Delta Lake
- Elasticsearch
- SAP HANA
- SingleStoreDB
- Snowflake
- Teradata

For more information, see [Adding a database](https://www.ibm.com/docs/SSDZ38_1.1.x/lh-console/topics/add_db.html). {: external}

## 7 July 2023
{: #lakehouse_july72023}

## Version 1.0.0
{: #version_100}

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
