---

copyright:
  years: 2022, 2023
lastupdated: "2023-07-07"

keywords: watsonx.data, data ingestion, source file

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

# About data ingestion
{: #load_ingest_data}

Data ingestion is the process of importing and loading data into {{site.data.keyword.lakehouse_full}}. You can use the **Create table** option from the **Data manager** page to load local or external sources of data files to create tables.
{: shortdesc}

When you ingest a data file into the {{site.data.keyword.lakehouse_short}}, the table schema is generated and inferred when a query is run.
Data ingestion in {{site.data.keyword.lakehouse_short}} supports CSV and Parquet formats. The files to be ingested must be of the same format type and same schema. The {{site.data.keyword.lakehouse_short}} auto-discovers the schema based on the source file being ingested.

## Loading or ingesting data through CLI
{: #load_ingest_datacli}

An ingestion job in {{site.data.keyword.lakehouse_short}} can be run with the **ibm-lh** tool. The tool must be pulled from the `ibm-lh-client` and installed in the local system to run the ingestion job through the CLI.

The **ibm-lh** tool supports the following features:

- Auto-discovery of schema based on the source file or target table.
- Advanced table configuration options for the CSV files:

   * Delimiter
   * Header
   * File encoding
   * Line delimiter
   * Escape characters

- Ingestion of a single, multiple file(s), or a single folder (no sub folders) of S3 and local Parquet file(s).
- Ingestion of a single, multiple file(s), or a single folder (no sub folders) of S3 and local CSV file(s).

Following are some of the requirements or limitations of the **ibm-lh** tool:

* Source files must have the same type of format.
* Schema evolution is not supported.
* Iceberg target table is the supported output format.
* Partitioning is not supported.
* IBM Cloud Object Storage (COS), AWS S3, and MinIO object storage are supported.
* pathStyleAccess property for object storage is not supported.
