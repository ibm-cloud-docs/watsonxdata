---

copyright:
  years: 2022, 2025
lastupdated: "2025-07-21"

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

**Applies to** : [Spark engine]{: tag-blue}  [Gluten accelerated Spark engine]{: tag-green}

This topic describes how to a run Spark job that helps to sync up Iceberg table data from Merge-on-Read (MoR) format to Copy-on-Write (CoW) format. Read operations are more efficient with Iceberg Copy-On-Write tables.
{: shortdesc}


You can use one of the following methods for the conversion:
- [Register COW Table](#sbmt_spk_mor_cowrcta) : This approach creates a named reference for the MoR table by using Iceberg [Register_table](https://www.ibm.com/links?url=https%3A%2F%2Ficeberg.apache.org%2Fdocs%2F1.6.0%2Fspark-procedures%2F%3Fh%3Dregister%23register_table) API, which points to a compacted consistent version of the MoR table and serves as the CoW table. This method is recommended and is more cost-effective.
- [Change Data Capture (CDC)](#sbmt_spk_mor_cowrcdc): This approach maintains two copies of the table. One is the MoR table where the updates are made and the second is a CoW table, which serves as a mirror of the MoR table. The Spark job retrieves the changes from MoR table between last synced snapshot and latest snapshot by using [Iceberg CDC](https://www.ibm.com/links?url=https%3A%2F%2Ficeberg.apache.org%2Fdocs%2F1.7.1%2Fspark-procedures%2F%23change-data-capture) procedure and merge them into CoW table. This approach is costlier than Register Table approach since it maintain a replica of MoR table.

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
- `<encoded-api-key>` : The value must be in the format echo -n"ibmlhapikey_<user_id>:<user’s api key>" | base64. Here, <user_id> is the IBM Cloud ID of the user whose api key is used to access the data bucket. The <IAM_APIKEY> here is the API key of the user accessing the Object store bucket. To generate an API key, login into the watsonx.data console and navigate to Profile > Profile and Settings > API Keys and generate a new API key.

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
- `<encoded-api-key>` : The value must be in the format echo -n"ibmlhapikey_<user_id>:<user’s api key>" | base64. Here, <user_id> is the IBM Cloud ID of the user whose api key is used to access the data bucket. The <IAM_APIKEY> here is the API key of the user accessing the Object store bucket. To generate an API key, login into the watsonx.data console and navigate to Profile > Profile and Settings > API Keys and generate a new API key.


### Default Hardware configuration
{: #spk_hrwr}


To manually specify the number of CPU cores (Driver and Executor) and memory that is required for the workload , below configs can be modified and passed in the payload:

```bash
"num-executors" : "1",
"spark.executor.cores": "1",
"spark.executor.memory": "4G",
"spark.driver.cores": "1",
"spark.driver.memory": "4G",
```
{: codeblock}

For details on enabling autoscaling, see [Enabling application autoscaling](/docs/watsonxdata?topic=watsonxdata-appl-auto-scaling).
