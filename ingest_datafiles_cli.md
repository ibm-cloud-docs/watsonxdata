---

copyright:
  years: 2022, 2024
lastupdated: "2024-04-30"

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

# Creating an ingestion job by using commands
{: #create_ingestioncli}

You can run the **ibm-lh** tool to ingest data into {{site.data.keyword.lakehouse_full}} through the command line interface (CLI). The commands to run the ingestion job and examples are listed in this topic.
{: shortdesc}

## Before you begin
{: #byb}

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

The commands must be run within the ibm-lh container. For more details and instructions to install `ibm-lh-client` package and use the **ibm-lh** tool for ingestion, see [Installing ibm-lh-client](https://www.ibm.com/docs/en/watsonxdata/1.0.x?topic=package-installing-lh-client){: external} and [Setting up the ibm-lh command-line utility](https://www.ibm.com/docs/en/watsonxdata/1.0.x?topic=package-setting-up-lh-cli-utility){: external}.
{: note}

To access IBM Cloud Object Storage (COS) and MinIO object storage, specify the ENDPOINT_URL to pass the corresponding url to the tool. For more information about IBM COS, see [Endpoints and storage locations](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-endpoints){: external}.
{: note}

Replace the absolute values in the command examples with the values applicable to your environment. See [Options and variables supported in **ibm-lh** tool](watsonxdata?topic=watsonxdata-cli_commands).
{: note}

Following are the details of the command line option to ingest data files from S3 or local location to {{site.data.keyword.lakehouse_short}} Iceberg table:

## Ingest a single CSV/Parquet file from S3 location by using command
{: #example1}

To ingest a single CSV/Parquet file from a S3 location, run the following command:

```bash
ibm-lh data-copy --source-data-files SOURCE_DATA_FILE \
--staging-location s3://lh-target/staging \
--target-tables TARGET_TABLES \
--ingestion-engine-endpoint INGESTION_ENGINE_ENDPOINT \
--dbuser DBUSER \
--dbpassword DBPASSWORD \
--create-if-not-exist
```
{: codeblock}

For example:
```bash
ibm-lh data-copy --source-data-files s3://cust-bucket/warehouse/a_source_file.parquet \
--staging-location s3://cust-bucket/warehouse/staging/ \
--target-tables iceberg_target_catalog.ice_schema.cust_tab1 \
--ingestion-engine-endpoint "hostname=localhost,port=8080" \
--create-if-not-exist
```
{: screen}

## Ingest multiple CSV/Parquet files and CSV folders from S3 location by using a command
{: #example2}

To ingest multiple CSV/Parquet files and CSV folders from a S3 location, run the following command:

```bash
ibm-lh data-copy --source-data-files SOURCE_DATA_FILE \
--staging-location s3://lh-target/staging \
--target-tables TARGET_TABLES \
--ingestion-engine-endpoint INGESTION_ENGINE_ENDPOINT \
--dbuser DBUSER \
--dbpassword DBPASSWORD \
--create-if-not-exist
```
{: codeblock}

For examples:
```bash
ibm-lh data-copy --source-data-files s3://cust-bucket/warehouse/a_source_file1.csv,s3://cust-bucket/warehouse/a_source_file2.csv \
--staging-location s3://cust-bucket/warehouse/staging/ \
--target-tables iceberg_target_catalog.ice_schema.cust_tab1 \
--ingestion-engine-endpoint "hostname=localhost,port=8080" \
--create-if-not-exist
```
{: screen}

```bash
ibm-lh data-copy --source-data-files s3://cust-bucket/warehouse/ \
--staging-location s3://cust-bucket/warehouse/staging/ \
--target-tables iceberg_target_catalog.ice_schema.cust_tab1 \
--ingestion-engine-endpoint "hostname=localhost,port=8080" \
--create-if-not-exist
```
{: screen}

## Ingest all Parquet files in a folder from S3 location by using a command
{: #example3}

To ingest all Parquet files in a folder from a S3 location, run the following command:

```bash
ibm-lh data-copy --source-data-files SOURCE_DATA_FILE \
--target-tables TARGET_TABLES \
--ingestion-engine-endpoint INGESTION_ENGINE_ENDPOINT \
--dbuser DBUSER \
--dbpassword DBPASSWORD \
--create-if-not-exist
```
{: codeblock}

For example:
```bash
ibm-lh data-copy --source-data-files s3://cust-bucket/warehouse/ \
--target-tables iceberg_target_catalog.ice_schema.cust_tab1 \
--ingestion-engine-endpoint "hostname=localhost,port=8080" \
--create-if-not-exist
```
{: screen}

In general, this option does not require a staging location. However, a few exceptional scenarios are there when a staging location must be specified. When the staging location is not used, make sure that the hive catalog configured with Presto can be used with source-data-files location. The following are the exceptional cases where a staging location is required:
- Any or all parquet files in the folder are huge.
- Any or all parquet files in the folder have special columns, such as TIME.
{: note}

## Ingest a CSV/Parquet file or folder from a local file system by using command.
{: #example4}

To ingest a single Parquet file from a local location, run the following command:

```bash
ibm-lh data-copy --source-data-files SOURCE_DATA_FILE \
--staging-location s3://lh-target/staging \
--target-tables TARGET_TABLES \
--ingestion-engine-endpoint INGESTION_ENGINE_ENDPOINT \
--dbuser DBUSER \
--dbpassword DBPASSWORD \
--create-if-not-exist
```
{: codeblock}

For example:
```bash
ibm-lh data-copy --source-data-files /cust-bucket/warehouse/a_source_file1.parquet \
--staging-location s3://cust-bucket/warehouse/staging/ \
--target-tables iceberg_target_catalog.ice_schema.cust_tab1 \
--ingestion-engine-endpoint "hostname=localhost,port=8080" \
--create-if-not-exist
```
{: screen}

```bash
ibm-lh data-copy --source-data-files /cust-bucket/warehouse/ \
--staging-location s3://cust-bucket/warehouse/staging/ \
--target-tables iceberg_target_catalog.ice_schema.cust_tab1 \
--ingestion-engine-endpoint "hostname=localhost,port=8080" \
--create-if-not-exist
```
{: screen}

## Ingest any data file from local file system by using a command
{: #example5}

To ingest any data file from a local location, run the following command:

To ingest any type of data files from a local file system, data files are needed to be copied to ~ /ibm-lh-client/localstorage/volumes/ibm-lh directory. Now, you can access data files from /ibmlhdata/ directory by using the `ibm-lh data-copy` command.
{: note}

```bash
ibm-lh data-copy --source-data-files SOURCE_DATA_FILE \" \
--staging-location s3://lh-target/staging \
--target-tables TARGET_TABLES \
--staging-hive-catalog <catalog_name> \
--schema <SCHEMA> \
--ingestion-engine-endpoint INGESTION_ENGINE_ENDPOINT \
--trust-store-path <TRUST_STORE_PATH> \
--trust-store-password <TRUST_STORE_PASSWORD> \
--dbuser DBUSER \
--dbpassword DBPASSWORD \
--create-if-not-exist
```
{: codeblock}

For example:
```bash
ibm-lh data-copy --source-data-files /ibmlhdata/reptile.csv \
--staging-location  s3://watsonx.data/staging \
--target-tables iceberg_data.ivt_sanity_test_1.reptile \
--staging-hive-catalog hive_test \
--schema /ibmlhdata/schema.cfg \
--ingestion-engine-endpoint "hostname=ibm-lh-lakehouse-presto-01-presto-svc-cpd-instance.apps.ivt384.cp.fyre.ibm.com,port=443" \
--trust-store-path /mnt/infra/tls/aliases/ibm-lh-lakehouse-presto-01-presto-svc-cpd-instance.apps.ivt384.cp.fyre.ibm.com:443.crt \
--trust-store-password changeit \
--dbuser xxxx\
--dbpassword xxxx \
--create-if-not-exist
```
{: screen}

## Ingest CSV or local Parquet or S3 Parquet files that use staging location
{: #example6}

To ingest CSV/local Parquet/S3 Parquet files that use staging location:

```bash
ibm-lh data-copy --source-data-files SOURCE_DATA_FILE \
--staging-location s3://lh-target/staging \
--target-tables TARGET_TABLES \
--staging-hive-catalog <catalog_name> \
--staging-hive-schema <schema_name> \
--ingestion-engine-endpoint INGESTION_ENGINE_ENDPOINT \
--trust-store-path <TRUST_STORE_PATH> \
--trust-store-password <TRUST_STORE_PASSWORD> \
--dbuser DBUSER \
--dbpassword DBPASSWORD \
--create-if-not-exist
```
{: codeblock}

For example:
```bash
ibm-lh data-copy --source-data-files s3://watsonx-data-0823-2/test_icos/GVT-DATA-C.csv \
--staging-location  s3://watsonx.data-staging \
--target-tables iceberg_data.test_iceberg.gvt_data_v \
--staging-hive-catalog staging_catalog \
--staging-hive-schema staging_schema \
--ingestion-engine-endpoint "hostname=ibm-lh-lakehouse-presto-01-presto-svc-cpd-instance.apps.ivt384.cp.fyre.ibm.com,port=443" \
--trust-store-path /mnt/infra/tls/aliases/ibm-lh-lakehouse-presto-01-presto-svc-cpd-instance.apps.ivt384.cp.fyre.ibm.com:443.crt \
--trust-store-password changeit \
--dbuser xxxx\
--dbpassword xxxx \
--create-if-not-exist
```
{: screen}

Here, `--staging-location` is `s3://watsonx.data-staging`. The `--staging-hive-catalog` that is `staging_catalog` must be associated with the bucket `watsonx.data-staging`.
