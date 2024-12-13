---

copyright:
  years: 2022, 2024
lastupdated: "2024-12-11"

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

# Ingesting data through command line - Spark REST API
{: #ingest_rstapi_cli}

You can run the **ibm-lh** tool to ingest data into {{site.data.keyword.lakehouse_full}} through the command line interface (CLI) using the IBM Analytics Engine (Spark) REST API. This CLI based ingestion uses REST endpoint to do the ingestion. This is the default mode of ingestion. The commands to run the ingestion job are listed in this topic.
{: shortdesc}

## Before you begin
{: #bybspkrstapi}

* You must have the Administrator role and privileges in the catalog to do ingestion through the web console.
* Add and register IBM Analytics Engine (Spark). See [Provisioning a Spark engine]({{site.data.keyword.ref-spl_engine-link}}).
* Add storage for the target catalog. See [Adding a storage-catalog pair]({{site.data.keyword.ref-reg_bucket-link}}).
* Create schema and table in the catalog for the data to be ingested. See [Creating schemas]({{site.data.keyword.ref-create_schema-link}}) and [Creating tables]({{site.data.keyword.ref-create_table-link}}).

## Procedure
{: #procdresprkapi}

1. Set the mandatory environment variable `ENABLED_INGEST_MODE` to `SPARK` before starting an ingestion job by running the following command:

   ```bash
   export ENABLED_INGEST_MODE=SPARK
   ```
   {: codeblock}

2. Set the optional environment variables from the following as required before starting an ingestion job by running the following commands:

   ```bash
   export IBM_LH_SPARK_EXECUTOR_CORES=1
   export IBM_LH_SPARK_EXECUTOR_MEMORY=2G
   export IBM_LH_SPARK_EXECUTOR_COUNT=1
   export IBM_LH_SPARK_DRIVER_CORES=1
   export IBM_LH_SPARK_DRIVER_MEMORY=2G
   ```
   {: codeblock}

   If IBM Analytics Engine Serverless instance on IBM Cloud is registered as external Spark on {{site.data.keyword.lakehouse_short}}, the Spark driver, executor vCPU and memory combinations must be in a 1:2, 1:4, or 1:8 ratio. See See [Default limits and quotas for Analytics Engine instances](https://cloud.ibm.com/docs/AnalyticsEngine?topic=AnalyticsEngine-limits).
   {: note}

   |Environment variable name|Description|
   |-------|-----|
   |`IBM_LH_SPARK_EXECUTOR_CORES`|Optional spark engine configuration setting for executor cores|
   |`IBM_LH_SPARK_EXECUTOR_MEMORY`|Optional spark engine configuration setting for executor memory|
   |`IBM_LH_SPARK_EXECUTOR_COUNT`|Optional spark engine configuration setting for executor count|
   |`IBM_LH_SPARK_DRIVER_CORES`|Optional spark engine configuration setting for driver cores|
   |`IBM_LH_SPARK_DRIVER_MEMORY`|Optional spark engine configuration setting for driver memory|
   {: caption="Table 1" caption-side="bottom"}

3. Run the following command to ingest data from a single or multiple source data files:

   ```bash
   ibm-lh data-copy --target-table iceberg_data.ice_schema.ytab \
   --source-data-files "s3://lh-ingest/hive/warehouse/folder_ingestion/" \
   --user someuser@us.ibm.com \
   --password **** \
   --url https://us-south.lakehouse.dev.cloud.ibm.com/ \
   --instance-id crn:v1:staging:public:lakehouse:us-south:a/fd160ae2ce454503af0d051dfadf29f3:25fdad6d-1576-4d98-8768-7c31e2452597:: \
   --schema /home/nz/config/schema.cfg \
   --engine-id spark214 \
   --log-directory /tmp/mylogs \
   --partition-by "<columnname1>, <columnname2> \
   --create-if-not-exist
   ```
   {: codeblock}

   Where the parameters used are listed as follows:

   |Parameter|Description|
   |------------|----------|
   |`--create-if-not-exist`|Use this option if the target schema or table is not created. Do not use if the target schema or table is already created.|
   |`--engine-id`|Engine id of Spark engine when using REST API based `SPARK` ingestion.|
   |`--instance-id`|Identify unique instances. In SaaS environment, CRN is the instance id.|
   |`--log-directory`|This option is used to specify the location of log files.|
   |`--partition-by`|This parameter supports the functions for years, months, days, hours for timestamp in the `partition-by` list. If a target table already exist or the `create-if-not-exist` parameter is not mentioned the partition-by shall not make any effect on the data.|
   |`--password`|Password of the user connecting to the instance. In SaaS, API key to the isntance is used.|
   |`--schema`|Use this option with value in the format path/to/csvschema/config/file. Use the path to a schema.cfg file which specifies header and delimiter values for CSV source file or folder.|
   |`--source-data-files`|Path to s3 parquet or CSV file or folder. Folder paths must end with “/”. File names are case sensitive.|
   |`--target-table`|Target table in format `<catalogname>.<schemaname>.<tablename>`.|
   |`--user`|User name of the user connecting to the instance.|
   |`--url`|Base url of the location of {{site.data.keyword.lakehouse_full}} cluster.|
   {: caption="Table 2" caption-side="bottom"}

   `ibm-lh data-copy` returns the value `0` when ingestion job is completed successfully. When ingestion job has failed, `ibm-lh data-copy` returns a non `0` value.
   {: tip}

4. Run the following command to get the status of the ingest job:

   ```bash
   ibm-lh get-status --job-id <Job-id> --instance-id --url --user --password
   ```
   {: codeblock}

   Where the parameter used is listed as follows:

   |Parameter|Description|
   |-----|----|
   |`--job-id<Job id>`|Job id is generated when REST API or UI based ingestion is initiated. This job id is used in getting the status of ingestion job. This parameter is used only used with `ibm-lh get-status` command. The short command for this parameter is `-j`.|
   {: caption="Table 3" caption-side="bottom"}

5. Run the following command to get the history of all ingestion jobs:

   ```bash
   ibm-lh get-status --all-jobs --instance-id --url --user --password
   ```
   {: codeblock}

   Where the parameter used is listed as follows:

   |Parameter|Description|
   |-----|----|
   |`--all-jobs`|This all-jobs parameter gives the history of all ingestion jobs. This parameter is used only used with `ibm-lh get-status` command.|
   {: caption="Table 4" caption-side="bottom"}


   `get-status` is supported with ibm-lh only in the interactive mode of ingestion.
   {: note}
