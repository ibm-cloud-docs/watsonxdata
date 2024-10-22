---

copyright:
  years: 2022, 2024
lastupdated: "2024-10-22"

keywords: watsonxdata, ingesting, object storage bucket, data files, table format. SQL query

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

# Preparing for ingesting data
{: #prepare_ingest_data}

This topic guides you through efficiently ingesting data manually from an external object storage into your {{site.data.keyword.lakehouse_full}} for querying. We support IBM Storage Ceph, IBM Cloud Object Storage (COS), AWS S3, and MinIO as the object storage buckets.
{: shortdesc}

Parquet and CSV are the supported file types.

You can ingest Parquet files directly for optimal performance and CSV files require a staging directory for conversion to Parquet format.

## Before you begin
{: #ingest_b4yb}

This tutorial requires:

   * S3 folder must be created with data files in it for ingesting. The best way to create an S3 folder is by using AWS CLI. The source folder must contain either all parquet file or all CSV files. Use AWS CLI to avoid hidden "0-byte" files that can cause ingestion issues. For detailed information on S3 folder creation, refer to [Organizing objects in the Amazon S3 console by using folders](https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-folders.html).
   * Staging folder must be specified for CSV files, individual file ingestion (Parquet or CSV) and local Parquet folders. Staging folder is not required for all files in an S3 folder (source folder ingestion). The exception for this case is when there are type differences between different types of parquet files in the S3 folder or when TIME data type is involved.
   * For ingestion job through CLI, the staging bucket must be the same bucket that is associated with the Hive catalog. Staging is possible only in the Hive catalog.

## About this task
{: #abt_task}

Scenario: You have a collection of data files in an S3 folder that you need to ingest into your IBM database. You need to run SQL query on data files that is in your object storage bucket.

The objectives of this tutorial are listed as follows:
   * Creating infrastructure within the watsonx.data service.
   * Establishing connection with the customer data storage.
   * Querying from the storage

You can use [Spark ingestion]({{site.data.keyword.ref-ingest_spark_ui-link}}) to ingest data.
{: note}

For detailed information on the usage of different parameters, see [Options and parameters supported in ibm-lh tool]({{site.data.keyword.ref-cli_commands-link}}), and for ingesting data files into {{site.data.keyword.lakehouse_short}} by using Spark CLI, commands and configuration file, see [Spark ingestion through ibm-lh tool command line]({{site.data.keyword.ref-ingest_spark_cli-link}}), [Creating an ingestion job by using commands]({{site.data.keyword.ref-create_ingestioncli-link}}), and [Creating an ingestion job by using the configuration file]({{site.data.keyword.ref-create_ingestconfig-link}}).
{: note}

## Procedure
{: #prcdre_manualingst}

### Ingesting Parquet or CSV files from an S3 Folder
{: #prcdre_manualingst1}

In this section, you have a collection of Parquet/CSV files in an S3 folder that you need to ingest into your IBM database.

1. Prepare the source S3 folder:
   * Use AWS CLI to copy the Parquet /CSV files into a common S3 folder. Avoid creating empty folders through the console to prevent hidden 0-byte files.
1. Specify staging directory (For CLI ingestion):
   * Provide the staging-location parameter to designate a staging directory for CSV or specific Parquet files to Parquet conversion. The ingest tool will create it if it does not exist.

   See [Staging location](watsonxdata?topic=watsonxdata-cli_commands#stag_loc){: external} for more details.
   {: note}

1. Create schema file to specify CSV file properties:
   * Provide the schema parameter to specify CSV file properties such as field delimiter, line delimiter, escape character, encoding and whether header exists in the CSV file.

   See [Schema file specifications](watsonxdata?topic=watsonxdata-cli_commands#schema_spec){: external} for more details.
   {: note}

1. Initiate server-mode ingestion:
   * Employ the CLI (server-mode) to start the ingestion process.
1. CSV or specific Parquet to Parquet conversion:
   * The ingest tool converts the specific Parquet or CSV files into Parquet format and stores them in the staging directory.

## Results
{: #result_manualingst1}

* Optimizes data transfer performance.
* Simplifies the ingestion process.
* Provides clear troubleshooting in case of errors.
