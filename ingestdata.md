---

copyright:
  years: 2022, 2025
lastupdated: "2026-01-30"

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

Data ingestion is the process of importing and loading data into {{site.data.keyword.lakehouse_full}}. From the user interface (UI) of {{site.data.keyword.lakehouse_short}}, you can use the **Ingest data** module from the **Data manager** page to securely and easily load data. Alternatively, you can also ingest local or remote data files to create tables by using the **Create table from file** option.
{: shortdesc}

When you ingest a data file into the {{site.data.keyword.lakehouse_short}}, the table schema is generated and inferred when a query is run. The files to be ingested must be of the same format type and same schema. {{site.data.keyword.lakehouse_short}} auto-discovers the schema based on the source file being ingested.

Following are some of the requirements or behavior of data ingestion:

* Schema evolution is not supported.
* The target table must be an iceberg format table.
* IBM Storage Ceph, IBM Cloud Object Storage (COS), AWS S3, and MinIO object storage are supported.
* `pathStyleAccess` property for object storage is not supported.
* .txt, .csv, Parquet, JSON, ORC, and Avro. file formats are supported as source data files.
* The maximum limit for the cumulative size of files must be within 500 MB for local ingestion.
* Parquet, JSON, ORC, and Avro. files exceeding 2 MB cannot be previewed, but they will still be ingested successfully.
* JSON files with complex nested objects and arrays shall not be previewed in the UI.
* Complex JSON files shall be ingested as-is, resulting in arrays as table entries. This is not recommended for optimal data visualization and analysis.
* Keys within JSON files must be enclosed in quotation marks for proper parsing and interpretation.

## Loading or ingesting data through CLI
{: #load_ingest_datacli}

The command `./cpdctl wx-data ingestion` in the IBM cpdctl is now used for all ingestion use cases. For more information about how to use IBM CPDCTL CLI, see [IBM cpdctl](/docs/watsonxdata?topic=watsonxdata-cpdctl_title).


The `./cpdctl wx-data ingestion`command supports the following features:

- Auto-discovery of schema based on the source file or target table.
- Advanced table configuration options for the CSV files:

   * Delimiter
   * Header
   * File encoding
   * Line delimiter
   * Escape characters

- Ingestion of a single, multiple files, or a single folder (no sub folders) of S3 and local Parquet files.
- Ingestion of a single, multiple files, or a single folder (no sub folders) of S3 and local CSV files.
