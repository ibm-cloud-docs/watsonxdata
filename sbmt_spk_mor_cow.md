---

copyright:
  years: 2022, 2025
lastupdated: "2026-02-25"

keywords: lakehouse, engine, watsonx.data
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

# Submitting Spark jobs for MoR to CoW conversion
{: #sbmt_spk_mor_cow}

**Applies to** : [Spark engine]{: tag-blue}  [Apache Gluten accelerated Spark engine]{: tag-green}

This topic describes how to a run Spark job that helps to sync up Iceberg table data from Merge-on-Read (MoR) format to Copy-on-Write (CoW) format. Read operations are more efficient with Iceberg Copy-On-Write tables.
{: shortdesc}


You can use one of the following methods for the conversion:
- [Register COW Table](#sbmt_spk_mor_cowrcta) : This approach creates a named reference for the MoR table by using Iceberg [Register_table](https://www.ibm.com/links?url=https%3A%2F%2Ficeberg.apache.org%2Fdocs%2F1.6.0%2Fspark-procedures%2F%3Fh%3Dregister%23register_table) API, which points to a compacted consistent version of the MoR table and serves as the CoW table. This method is recommended and is more cost-effective.
- [Change Data Capture (CDC)](#sbmt_spk_mor_cowrcdc): This approach maintains two copies of the table. One is the MoR table where the updates are made and the second is a CoW table, which serves as a mirror of the MoR table. The Spark job retrieves the changes from MoR table between last synced snapshot and latest snapshot by using [Iceberg CDC](https://www.ibm.com/links?url=https%3A%2F%2Ficeberg.apache.org%2Fdocs%2F1.7.1%2Fspark-procedures%2F%23change-data-capture) procedure and merge them into CoW table. This approach is costlier than Register Table approach since it maintain a replica of MoR table.

The CDC approach is deprecated and will be removed in a future release. Use the Register COW Table approach for all new implementations.
{: note}

## About this task
{: #sbmt_spk_mor_cowatt}

### Register COW Table approach
{: #sbmt_spk_mor_cowrcta}

If you have a Merge-on-Read (MoR) table, you can specify the necessary parameter values and use the following sample payload to run the conversion job. The job syncs up the Iceberg operations in the MoR table and generates a compact Cow table.

```bash
{
    "application_details": {
        "application": "/opt/ibm/spark/builtin-apps/iceberg/iceberg-apps.jar",
        "class": "com.ibm.iceberg.apps.RegisterCowTable",
        "arguments": [
            "--catalog","<catalog-name>",
            "--database","<database-name>",
            "--mor-table","<mor-table-name>",
            "--cow-table","<cow-table-name>"
        ],
        "conf": {
            "spark.hadoop.wxd.apikey" : "Basic <encoded-api-key>"
        },
    }
}
```
{: codeblock}

Parameter values:
- `<catalog-name>`: The Iceberg catalog where the MoR table is available.
- `<database-name>` : The database where the MoR table is available.
- `<mor-table-name>` : The name of the MoR table.
- `<cow-table-name>` : The name of the CoW table that is synchronized with the MoR table.
- `<encoded-api-key>` : The value must be in the format echo -n"ibmlhapikey_<user_id>:<user’s api key>" | base64. Here, <user_id> is the IBM Cloud ID of the user whose api key is used to access the data bucket. The <IAM_APIKEY> here is the API key of the user accessing the Object store bucket. To generate an API key, login into the {{site.data.keyword.lakehouse_short}} console and navigate to Profile > Profile and Settings > API Keys and generate a new API key.

## Additional conversion modes
{: #sbmt_spk_mor_cowrcta1}

These conversion modes are available starting with {{site.data.keyword.lakehouse_short}} version 2.3.1.
{: note}

The Register COW Table approach supports additional conversion modes beyond the original single table conversion:

1. [Multiple Tables Mode](#sbmt_spk_mor_cowrcta2): Convert multiple MoR tables in a single job execution
2. [Schema Level Mode](#sbmt_spk_mor_cowrcta3): Convert all MoR tables within a schema
3. [Batch Conversion Mod](#sbmt_spk_mor_cowrcta3): Process multiple schemas or tables using a batch configuration file


### Multiple Tables Mode
{: #sbmt_spk_mor_cowrcta2}

Convert multiple MoR tables within the same schema in a single job execution by providing a comma-separated list of table names.

**Sample payload:**

```bash
{
  "application_details": {
    "application": "/opt/ibm/spark/builtin-apps/iceberg/iceberg-apps.jar",
    "class": "com.ibm.iceberg.apps.RegisterCowTable",
    "arguments": [
      "--catalog", "<catalog-name>",
      "--schema", "<database-name>",
      "--mor_table", "<table1>,<table2>,<table3>"
    ],
    "conf": {
      "spark.hadoop.wxd.apikey": "Basic <encoded key>"
    }
  }
}
```
{: codeblock}

**Parameter values:**

- `<catalog-name>`: The Iceberg catalog where the MoR tables are available.
- `<database-name>`: The database where the MoR tables are available.
- `<table1>,<table2>,<table3>`: Comma-separated list of MoR table names to convert.
- `<encoded key>`: The value must be in the format echo -n"ibmlhapikey_<user_id>:<user’s api key>" | base64. Here, <user_id> is the IBM Cloud ID of the user whose api key is used to access the data bucket. The <IAM_APIKEY> here is the API key of the user accessing the Object store bucket. To generate an API key, login into the {{site.data.keyword.lakehouse_short}} console and navigate to Profile > Profile and Settings > API Keys and generate a new API key.

**Optional Arguments:**

- `--parallelism`: Number of parallel syncs.
- `--output_path`: Output path for sync results Parquet file.

When using Multiple Tables Mode, the CoW table names are automatically generated as `{morTable}_cow` for each MoR table. Individual CoW table names cannot be specified in this mode.
{: note}

### Schema Level Mode
{: #sbmt_spk_mor_cowrcta3}

Convert all MoR tables within a schema by specifying only the schema name. This mode automatically identifies and converts all MoR format tables in the specified schema.

**Sample payload:**

```bash
{
  "application_details": {
    "application": "/opt/ibm/spark/builtin-apps/iceberg/iceberg-apps.jar",
    "class": "com.ibm.iceberg.apps.RegisterCowTable",
    "arguments": [
      "--catalog", "<catalog-name>",
      "--schema", "<database-name>"
    ],
    "conf": {
      "spark.hadoop.wxd.apikey": "Basic <encoded key>"
    }
  }
}
```
{: codeblock}

**Parameter values:**

- `<catalog-name>`: The Iceberg catalog where the schema is available.
- `<database-name>`: The schema name containing MoR tables to convert.
- `<encoded key>`: The value must be in the format echo -n"ibmlhapikey_<user_id>:<user’s api key>" | base64. Here, <user_id> is the IBM Cloud ID of the user whose api key is used to access the data bucket. The <IAM_APIKEY> here is the API key of the user accessing the Object store bucket. To generate an API key, login into the {{site.data.keyword.lakehouse_short}} console and navigate to Profile > Profile and Settings > API Keys and generate a new API key.

**Optional Arguments:**

- `--parallelism`: Number of parallel syncs.
- `--output_path`: Output path for sync results Parquet file.

### Batch Conversion Mode
{: #sbmt_spk_mor_cowrcta4}

Process multiple schemas or tables using a batch configuration file. This mode is useful for large-scale conversions across multiple schemas or catalogs.

**Sample payload:**

```bash
{
  "application_details": {
    "application": "/opt/ibm/spark/builtin-apps/iceberg/iceberg-apps.jar",
    "class": "com.ibm.iceberg.apps.RegisterCowTable",
    "arguments": [
      "--sync_json", "<path-to-sync-json>",
      "--output_path", "<path-to-sync_results>"
    ],
    "conf": {
      "spark.hadoop.wxd.apikey": "Basic <encoded key>"
    }
  }
}
```
{: codeblock}

**Parameter values:**

- `<path-to-sync-json>`: Path to the sync json file containing the list of catalogs, schemas, and tables to process.
- `<encoded key>`: The value must be in the format echo -n"ibmlhapikey_<user_id>:<user’s api key>" | base64. Here, <user_id> is the IBM Cloud ID of the user whose api key is used to access the data bucket. The <IAM_APIKEY> here is the API key of the user accessing the Object store bucket. To generate an API key, login into the {{site.data.keyword.lakehouse_short}} console and navigate to Profile > Profile and Settings > API Keys and generate a new API key.

**Optional Arguments:**

- `--parallelism`: Number of parallel syncs.
- `--output_path`: Output path for sync results Parquet file.


**Sync json configuration file format:**

```bash
{
  "syncs": [
    {
      "catalog": "<catalog_name>",
      "schema": "<schema_name>",
      "morTable": "<mor_table_name>",
      "cowTable": "<cow_table_name>"
    },
    {
      "catalog": "<another_catalog_name>",
      "schema": "<another_schema_name>",
      "morTable": "<another_mor_table_name>"
    }
  ]
}
```
{: codeblock}

When using Batch Conversion Mode, the CoW table parameter is optional. If not provided, the CoW table name is automatically generated as `{morTable}_cow` for each MoR table.
{: note}

### Change Data Capture (CDC) approach
{: #sbmt_spk_mor_cowrcdc}

If you have a Merge-on-Read (MoR) table, you can specify the necessary parameter values and use the following sample payload to run the conversion job. The job syncs up the Iceberg operations in the MoR table and generates a compact Cow table.

```bash
{
    "application_details": {
        "application": "/opt/ibm/spark/builtin-apps/iceberg/iceberg-apps.jar",
        "class": "com.ibm.iceberg.apps.CDCSync",
        "arguments": [
            "--catalog","<catalog-name>",
            "--database","<database-name>",
            "--mor-table","<mor-table-name>",
            "--cow-table","<cow-table-name>",
            "--primary-key","<primary-key>"
        ],
        "conf": {
            "spark.hadoop.wxd.apikey" : "Basic <encoded-api-key>",
        }
    }
}
```
{: codeblock}

Parameter values:
- `<catalog-name>`: The Iceberg catalog where the MoR table is available.
- `<database-name>` : The database where the MoR table is available.
- `<mor-table-name>` : The name of the MoR table.
- `<cow-table-name>` : The name of the CoW table that is synchronized with the MoR table.
- `<primary-key>` : The primary key that is used for creating CoW table.
- `<encoded-api-key>` : The value must be in the format echo -n"ibmlhapikey_<user_id>:<user’s api key>" | base64. Here, <user_id> is the IBM Cloud ID of the user whose api key is used to access the data bucket. The <IAM_APIKEY> here is the API key of the user accessing the Object store bucket. To generate an API key, login into the {{site.data.keyword.lakehouse_short}} console and navigate to Profile > Profile and Settings > API Keys and generate a new API key.
