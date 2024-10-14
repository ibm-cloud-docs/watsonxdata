---

copyright:
  years: 2022, 2024
lastupdated: "2024-10-06"

keywords: watsonxdata, staging, config file, target iceberg table, parquet, csv, command line, cli

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

# Config file ingestion in Presto ingestion mode
{: #create_ingestconfig}

You can run the **ibm-lh** tool to ingest data into {{site.data.keyword.lakehouse_full}} through the CLI. The configuration file and examples are listed in this topic.
{: shortdesc}

## Before you begin:
{: #bybconfig}

Set the mandatory environment variable `ENABLED_INGEST_MODE` to `PRESTO` before starting an ingestion job by running the following command:

```bash
export ENABLED_INGEST_MODE=PRESTO
```
{: codeblock}

Set the environment variables for `SOURCE_S3_CREDS` and `STAGING_S3_CREDS` based on the requirements before starting an ingestion job by running the following commands:

```bash
export SOURCE_S3_CREDS="AWS_ACCESS_KEY_ID=,AWS_SECRET_ACCESS_KEY=,ENDPOINT_URL=,AWS_REGION=,BUCKET_NAME="
```
{: codeblock}

```bash
export STAGING_S3_CREDS="AWS_ACCESS_KEY_ID=,AWS_SECRET_ACCESS_KEY=,ENDPOINT_URL=,AWS_REGION=,BUCKET_NAME="
```
{: codeblock}

## About this task
{: #attask}

To run the ingestion jobs, you can use the configuration file option. Advantage of using a configuration file is that, multiple ingestion jobs can be completed in a single starting of the ingestion tool.

Run the following command to do multiple ingestion jobs after you update the configuration file:

   ```bash
   ibm-lh data-copy --ingest-config /<your_ingest_configfilename>
   ```
   {: codeblock}

The commands must be run within the **ibm-lh** container. For more details and instructions to install `ibm-lh-client` package and use the **ibm-lh** tool for ingestion, see [Installing ibm-lh-client](https://www.ibm.com/docs/en/watsonx/watsonxdata/2.0.x?topic=package-installing-lh-client){: external} and [Setting up the ibm-lh command-line utility](https://www.ibm.com/docs/en/watsonx/watsonxdata/2.0.x?topic=package-setting-up-lh-cli-utility){: external}.
{: note}

To access IBM Cloud Object Storage (COS) and MinIO object storage, specify the ENDPOINT_URL to pass the corresponding url to the tool. For more information about IBM COS, see [Endpoints and storage locations](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-endpoints){: external}.
{: note}

Replace the absolute values inside angular brackets of command examples with values applicable to your environment. See [Options and variables supported in **ibm-lh** tool]({{site.data.keyword.ref-cli_commands-link}}).
{: note}

Following are the details of the config file option to ingest data files from S3 or local location to {{site.data.keyword.lakehouse_short}} Iceberg table:

## Ingest a single CSV/Parquet file from S3 location by using config file
{: #ingest1}

To ingest a single Parquet file from a S3 location, run the following command:

```bash
[global-ingest-config]
target-table:table_name
ingestion-engine:hostname=<hostname>,port=<port>
create-if-not-exist:<true>
[ingest-config1]
source-files:SOURCE_DATA_FILE
staging-location:STAGING_LOCATION
```
{: codeblock}

For example:
```bash
[global-ingest-config]
target-table:iceberg_cat.ice_schema.customer1_tab
ingestion-engine:hostname=localhost,port=8080
create-if-not-exist:true

[ingest-config1]
source-files:s3://cust-bucket/warehouse/a_source_file.parquet
staging-location:s3://cust-bucket/warehouse/staging/
```
{: screen}

## Ingest multiple CSV/Parquet files and CSV folders from S3 location by using config file
{: #ingest2}

To ingest multiple Parquet files from a S3 location, run the following command:

```bash
[global-ingest-config]
target-table:table_name
ingestion-engine:hostname=<hostname>,port=<port>
create-if-not-exist:<true>
[ingest-config1]
source-files:SOURCE_DATA_FILE
staging-location:STAGING_LOCATION
```
{: codeblock}

For example:
```bash
[global-ingest-config]
target-table:iceberg_cat.ice_schema.customer1_tab
ingestion-engine:hostname=localhost,port=8080
create-if-not-exist:true

[ingest-config1]
source-files:s3://cust-bucket/warehouse/a_source_file1.csv,s3://cust-bucket/warehouse/a_source_file2.csv
staging-location:s3://cust-bucket/warehouse/staging/
```
{: screen}

```bash
[global-ingest-config]
target-table:iceberg_cat.ice_schema.customer1_tab
ingestion-engine:hostname=localhost,port=8080
create-if-not-exist:true

[ingest-config1]
source-files:s3://cust-bucket/warehouse/
staging-location:s3://cust-bucket/warehouse/staging/
```
{: screen}

## Ingest all Parquet files in a folder from S3 location by using config file
{: #ingest3}

To ingest all Parquet files in a folder from a S3 location, run the following command:

```bash
[global-ingest-config]
target-table:table_name
ingestion-engine:hostname=<hostname>,port=<port>
create-if-not-exist:<true>
[ingest-config1]
source-files:SOURCE_DATA_FILE
```
{: codeblock}

For example:
```bash
[global-ingest-config]
target-table:iceberg_cat.ice_schema.customer1_tab
ingestion-engine:hostname=localhost,port=8080
create-if-not-exist:true

[ingest-config1]
source-files:s3://cust-bucket/warehouse/
```
{: screen}

In general, this option does not require a staging location. However, a few exceptional scenarios are there when a staging location must be specified. When the staging location is not used, make sure that the hive catalog configured with Presto can be used with source-files location. The following are the exceptional cases where a staging location is required:
- Any or all parquet files in the folder are huge.
- Any or all parquet files in the folder have special columns, such as TIME.
{: note}

## Ingest a CSV/Parquet file or a folder of files from a local file system by using config file
{: #ingest4}

To ingest a single CSV file from a local location, run the following command:

```bash
[global-ingest-config]
target-table:table_name
ingestion-engine:hostname=<hostname>,port=<port>
create-if-not-exist:<true>
[ingest-config1]
source-files:SOURCE_DATA_FILE
staging-location:STAGING_LOCATION
```
{: codeblock}

For example:
```bash
[global-ingest-config]
target-table:iceberg_cat.ice_schema.customer1_tab
ingestion-engine:hostname=localhost,port=8080
create-if-not-exist:true

[ingest-config1]
source-files:/tmp/customer1.parquet
staging-location:s3://cust-bucket/warehouse/staging/
```
{: screen}

```bash
[global-ingest-config]
target-table:iceberg_cat.ice_schema.customer1_tab
ingestion-engine:hostname=localhost,port=8080
create-if-not-exist:true

[ingest-config1]
source-files:/tmp/
staging-location:s3://cust-bucket/warehouse/staging/
```
{: screen}

## Ingest any data file from local file system by using a config file
{: #ingest5}

To ingest any data file from a local location, run the following command:

To ingest any type of data files from a local file system, data files are needed to be copied to ~ /ibm-lh-client/localstorage/volumes/ibm-lh directory. Now, you can access data files from /ibmlhdata/ directory by using the `ibm-lh data-copy` command.
{: note}

```bash
[global-ingest-config]
target-table:table_name
ingestion-engine:hostname=<hostname>,port=<port>
create-if-not-exist:<true>

[ingest-config1]
source-files:SOURCE_DATA_FILE
staging-location:STAGING_LOCATIONstaging-hive-catalog:<catalog_name>
schema:<SCHEMA>
dbuser:<DBUSER>
dbpassword:<DBPASSWORD>
trust-store-path:<TRUST_STORE_PATH>
trust-store-password:<TRUST_STORE_PASSWORD>
```
{: codeblock}

For example:
```bash
[global-ingest-config]
target-table:iceberg_data.ivt_sanity_test_1.reptile
ingestion-engine:hostname=ibm-lh-lakehouse-presto-01-presto-svc-cpd-instance.apps.ivt384.cp.fyre.ibm.com,port=443
create-if-not-exist:true

[ingest-config1]
source-files:/ibmlhdata/reptile.csv
staging-location:s3://watsonx.data/staging
staging-hive-catalog:hive_test
schema:schema.cfg
dbuser:xxxx
dbpassword:xxxx
trust-store-path:/mnt/infra/tls/aliases/ibm-lh-lakehouse-presto-01-presto-svc-cpd-instance.apps.ivt384.cp.fyre.ibm.com:443.crt
trust-store-password:changeit
```
{: screen}

## Ingest CSV/local Parquet/S3 Parquet files that use staging location.
{: #ingest6}

To ingest CSV/local Parquet/S3 Parquet files that use staging location:

```bash
[global-ingest-config]
target-table:table_name
ingestion-engine:hostname=<hostname>,port=<port>
create-if-not-exist:<true>

[ingest-config1]
source-files:SOURCE_DATA_FILE
staging-location:STAGING_LOCATION
staging-hive-catalog:<catalog_name>
schema:<SCHEMA>
dbuser:<DBUSER>
dbpassword:<DBPASSWORD>
trust-store-path:<TRUST_STORE_PATH>
trust-store-password:<TRUST_STORE_PASSWORD>
```
{: codeblock}

For example:
```bash
[global-ingest-config]
target-table:iceberg_data.test_iceberg.gvt_data_v
ingestion-engine:hostname=ibm-lh-lakehouse-presto-01-presto-svc-cpd-instance.apps.ivt384.cp.fyre.ibm.com,port=443
create-if-not-exist:true

[ingest-config1]
source-files:s3://watsonx-data-0823-2/test_icos/GVT-DATA-C.csv
staging-location:s3://watsonx.data-staging
staging-hive-catalog:staging_catalog
staging-hive-schema:staging_schema
dbuser:xxxx
dbpassword:xxxx
trust-store-path:/mnt/infra/tls/aliases/ibm-lh-lakehouse-presto-01-presto-svc-cpd-instance.apps.ivt384.cp.fyre.ibm.com:443.crt
trust-store-password:changeit
```
{: screen}

Here, `--staging-location` is `s3://watsonx.data-staging`. The `--staging-hive-catalog` that is `staging_catalog` must be associated with the storage bucket `watsonx.data-staging`.
