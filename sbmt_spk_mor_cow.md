---

copyright:
  years: 2022, 2025
lastupdated: "2025-06-04"

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

This topic provides the steps required to locate and view Spark logs associated with submitted ingestion jobs within {{site.data.keyword.lakehouse_full}}. By accessing these logs, you can gain valuable insights into the execution details, potential error messages related to the ingestion process, and troubleshooting ingestion jobs.
{: shortdesc}

You can use one of the following methods for the conversion:
- [Register COW Table](https://ibmdocs.dcs.ibm.com/docs/en/SSDZ38_2.2.x_test?topic=engine-submitting-spark-jobs-mor-cow-conversion#mor_cow__RT) : This approach creates a named reference for the MoR table by using Iceberg [Register_table](https://www.ibm.com/links?url=https%3A%2F%2Ficeberg.apache.org%2Fdocs%2F1.6.0%2Fspark-procedures%2F%3Fh%3Dregister%23register_table) API, which points to a compacted consistent version of the MoR table and serves as the CoW table. This method is recommended and is more cost-effective.
- [Change Data Capture (CDC)](https://ibmdocs.dcs.ibm.com/docs/en/SSDZ38_2.2.x_test?topic=engine-submitting-spark-jobs-mor-cow-conversion#mor_cow__CDC): This approach maintains two copies of the table. One is the MoR table where the updates are made and the second is a CoW table, which serves as a mirror of the MoR table. The Spark job retrieves the changes from MoR table between last synced snapshot and latest snapshot by using [Iceberg CDC](https://www.ibm.com/links?url=https%3A%2F%2Ficeberg.apache.org%2Fdocs%2F1.7.1%2Fspark-procedures%2F%23change-data-capture) procedure and merge them into CoW table. This approach is costlier than Register Table approach since it maintain a replica of MoR table.

## Before you begin
{: #sbmt_spk_mor_cowbyb}

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
            "ae.spark.autoscale.enable":"false",
            "num-executors" : "1",
            "spark.executor.cores": "4",
            "spark.executor.memory": "16G",
            "spark.driver.cores": "4",
            "spark.driver.memory": "16G",
            "ae.spark.driver.log.level":"INFO",
            "ae.spark.executor.log.level":"INFO",
            "spark.hadoop.wxd.apikey" : "xx"
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
            "ae.spark.autoscale.enable":"false",
            "num-executors" : "1",
            "spark.executor.cores": "4",
            "spark.executor.memory": "16G",
            "spark.driver.cores": "4",
            "spark.driver.memory": "16G",
            "ae.spark.driver.log.level":"INFO",
            "ae.spark.executor.log.level":"INFO",
            "spark.hadoop.wxd.apikey" : "xx"
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
