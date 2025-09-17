---

copyright:
  years: 2022, 2025
lastupdated: "2025-09-17"

keywords: watsonxdata, data explorer, associated catalogs, iceberg tables, data sample, time travel information, ingestion hub

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

# About Data manager
{: #exp_objects}

The **Data manager** page in {{site.data.keyword.lakehouse_full}} is the entry point to browse the schemas and tables by engine. You can select an engine by selecting the **Browse data** tab to view the associated catalogs, schemas, and tables.
{: shortdesc}

From the **Data manager** page, you can create schemas and tables by using the **Create** option. You can also select a catalog or schema, click the overflow menu, and use the corresponding **Create** option to create a schema or table. **Create table from file** option in the overflow menu of schema is also used to ingest a data file into {{site.data.keyword.lakehouse_short}}. Similarly, schemas and tables can be dropped from the catalogs.

Wait for a few minutes to view the changes after a schema or table is dropped.
{: note}

You can **Ingest data** from the **Data manager** page.
Other tasks that can be performed in the **Data manager** page include adding, renaming, or dropping a column.

You can browse the **Table schema** and up to 25 rows of **Data sample** for some tables. You can view the **Time travel** snapshots and use the **Rollback to snapshot** feature to rollback or rollforward to any snapshots for Iceberg tables.

{{site.data.keyword.lakehouse_short}} provides pre-defined **Sample and benchmarking data**, such as **tpch** and **tpcds**, to test the performance of a database system under controlled conditions. It also provides **System monitoring data** that uses **jmx** and **system** metrics to collect data about the system's health and performance during benchmark testing to understand how the system responds to the workload. **Sample and benchmarking data**, **tpch** and **tpcds** can only be queried using the Presto engines.

## Related API
{: #datamanager_api}

For information on related API, see
* [List all registered catalogs](https://cloud.ibm.com/apidocs/watsonxdata-software#list-catalogs)
* [Get catalog properties by catalog_id](https://cloud.ibm.com/apidocs/watsonxdata-software#get-catalog)
* [List all columns of a table](https://cloud.ibm.com/apidocs/watsonxdata-software#list-columns)
* [Add column](https://cloud.ibm.com/apidocs/watsonxdata-software#create-columns)
* [Delete column](https://cloud.ibm.com/apidocs/watsonxdata-software#delete-column)
* [Alter column](https://cloud.ibm.com/apidocs/watsonxdata-software#update-column)
* [Get table snapshots](https://cloud.ibm.com/apidocs/watsonxdata-software#list-table-snapshots)
* [Rollback table to snapshot](https://cloud.ibm.com/apidocs/watsonxdata-software#rollback-table)
