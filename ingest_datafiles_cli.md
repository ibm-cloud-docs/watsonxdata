---

copyright:
  years: 2022, 2023
lastupdated: "2023-07-07"

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

After installing the **ibm-lh** tool, you can run the tool to ingest data into {{site.data.keyword.lakehouse_full}} through the CLI. The commands to run the ingestion job and examples are listed in this topic.
{: shortdesc}

To access IBM Cloud Object Storage (COS) and MinIO object storage, specify the ENDPOINT_URL in --source-s3-creds and --staging-s3-creds to pass the corresponding url to the tool. For more information about IBM COS, see https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-endpoints.
{: note}

Replace the absolute values inside the angular brackets of command examples or config file examples with the values applicable to your environment. See [Options and variables supported in **ibm-lh** tool](watsonxdata?topic=watsonxdata-cli_commands).
{: note}

Following are the details of the command line option to ingest data files from S3 or local location to {{site.data.keyword.lakehouse_short}} Iceberg table:

## Ingest a single CSV/Parquet file from S3 location by using a command
{: #example1}

To ingest a single CSV/Parquet file from a S3 location, run the following command:

```bash
ibm-lh data-copy --source-data-files <SOURCE_DATA_FILE> --source-s3-creds "AWS_SECRET_ACCESS_KEY=<YOUR_SECRET_ASSESS_KEY>,AWS_ACCESS_KEY_ID=<YOUR_ACCESS_KEY_ID>,AWS_REGION=<YOUR_REGION>, BUCKET_NAME=<YOUR_BUCKET>, ENDPOINT_URL=<YOUR_ENDPOINT_URL>" --staging-location <STAGING_LOCATION> --staging-s3-creds "AWS_SECRET_ACCESS_KEY=<YOUR_TARGET_SECRET_ASSESS_KEY>,AWS_ACCESS_KEY_ID=<YOUR_TARGET_ACCESS_KEY_ID>,AWS_REGION=<YOUR_TARGET_REGION>, BUCKET_NAME=<YOUR_TARGET_BUCKET>, ENDPOINT_URL=<YOUR_TARGET_ENDPOINT_URL>” --target-tables <TARGET_TABLES> --ingestion-engine-endpoint <INGESTION_ENGINE_ENDPOINT> --dbuser <DBUSER> --dbpassword <DBPASSWORD> --create-if-not-exist
```
{: codeblock}

For example:
```bash
ibm-lh data-copy --source-data-files s3://cust-bucket/warehouse/a_source_file.parquet --source-s3-creds "AWS_ACCESS_KEY_ID=xxxxxx,AWS_SECRET_ACCESS_KEY=yyyyyy,AWS_REGION=us-east-1,BUCKET_NAME=cust-bucket" --staging-location s3://cust-bucket/warehouse/staging/ --staging-s3-creds "AWS_ACCESS_KEY_ID=zzzzzz,AWS_SECRET_ACCESS_KEY=vvvvvvv,AWS_REGION=us-east-1,BUCKET_NAME=cust-bucket" --target-tables iceberg_target_catalog.ice_schema.cust_tab1 --ingestion-engine-endpoint "hostname=localhost,port=8080" --create-if-not-exist
```
{: screen}

## Ingest multiple CSV/Parquet files and CSV folders from S3 location by using a command
{: #example2}

To ingest multiple CSV/Parquet files and CSV folders from a S3 location, run the following command:

```bash
ibm-lh data-copy --source-data-files <SOURCE_DATA_FILE> --source-s3-creds "AWS_SECRET_ACCESS_KEY=<YOUR_SECRET_ASSESS_KEY>, AWS_ACCESS_KEY_ID=<YOUR_ACCESS_KEY_ID>,AWS_REGION=<YOUR_REGION>, BUCKET_NAME=<YOUR_BUCKET>, ENDPOINT_URL=<YOUR_ENDPOINT_URL>" --staging-location <STAGING_LOCATION> --staging-s3-creds "AWS_SECRET_ACCESS_KEY=<YOUR_TARGET_SECRET_ASSESS_KEY>,AWS_ACCESS_KEY_ID=<YOUR_TARGET_ACCESS_KEY_ID>,AWS_REGION=<YOUR_TARGET_REGION>, BUCKET_NAME=<YOUR_TARGET_BUCKET>, ENDPOINT_URL=<YOUR_TARGET_ENDPOINT_URL>” --target-tables <TARGET_TABLES> --ingestion-engine-endpoint <INGESTION_ENGINE_ENDPOINT> --dbuser <DBUSER> --dbpassword <DBPASSWORD> --create-if-not-exist
```
{: codeblock}

For example:
```bash
ibm-lh data-copy --source-data-files s3://cust-bucket/warehouse/a_source_file1.csv, s3://cust-bucket/warehouse/a_source_file2.csv --source-s3-creds "AWS_ACCESS_KEY_ID=xxxxxx,AWS_SECRET_ACCESS_KEY=yyyyyy,AWS_REGION=us-east-1,BUCKET_NAME=cust-bucket" --staging-location s3://cust-bucket/warehouse/staging/ --staging-s3-creds "AWS_ACCESS_KEY_ID=zzzzzz,AWS_SECRET_ACCESS_KEY=vvvvvvv,AWS_REGION=us-east-1,BUCKET_NAME=cust-bucket" --target-tables iceberg_target_catalog.ice_schema.cust_tab1 --ingestion-engine-endpoint "hostname=localhost,port=8080" --create-if-not-exist
```
{: screen}

```bash
ibm-lh data-copy --source-data-files s3://cust-bucket/warehouse/ --source-s3-creds "AWS_ACCESS_KEY_ID=xxxxxx,AWS_SECRET_ACCESS_KEY=yyyyyy,AWS_REGION=us-east-1,BUCKET_NAME=cust-bucket" --staging-location s3://cust-bucket/warehouse/staging/ --staging-s3-creds "AWS_ACCESS_KEY_ID=zzzzzz,AWS_SECRET_ACCESS_KEY=vvvvvvv,AWS_REGION=us-east-1,BUCKET_NAME=cust-bucket" --target-tables iceberg_target_catalog.ice_schema.cust_tab1 --ingestion-engine-endpoint "hostname=localhost,port=8080" --create-if-not-exist
```
{: screen}

## Ingest all Parquet files in a folder from S3 location by using a command
{: #example3}

To ingest all Parquet files in a folder from a S3 location, run the following command:

```bash
ibm-lh data-copy --source-data-files <SOURCE_DATA_FILE> --source-s3-creds "AWS_SECRET_ACCESS_KEY=<YOUR_SECRET_ASSESS_KEY>,AWS_ACCESS_KEY_ID=<YOUR_ACCESS_KEY_ID>,AWS_REGION=<YOUR_REGION>, BUCKET_NAME=<YOUR_BUCKET, ENDPOINT_URL=<YOUR_ENDPOINT_URL>>" --target-tables <TARGET_TABLES> --ingestion-engine-endpoint <INGESTION_ENGINE_ENDPOINT> --dbuser <DBUSER> --dbpassword <DBPASSWORD> --create-if-not-exist
```
{: codeblock}

For example:
```bash
ibm-lh data-copy --source-data-files s3://cust-bucket/warehouse/ --source-s3-creds "AWS_ACCESS_KEY_ID=xxxxxx,AWS_SECRET_ACCESS_KEY=yyyyyy,AWS_REGION=us-east-1,BUCKET_NAME=cust-bucket" --target-tables iceberg_target_catalog.ice_schema.cust_tab1 --ingestion-engine-endpoint "hostname=localhost,port=8080" --create-if-not-exist
```
{: screen}

In general, this option does not require a staging location. However, there are a few exception scenarios when a staging location must be specified. When the staging location is not used, ensure that the hive catalog configured with Presto can be used with source-data-files location. Following are the exception cases where staging location is required:
- Any or all of the parquet files in the folder are huge.
- Any or all of the parquet files in the folder have special columns, such as date or decimal.
{: note}

## Ingest a  CSV/Parquet file or folder from a local file system by using a command
{: #example4}

To ingest a CSV/Parquet file or a folder of files from a local file system, run the following command:

```bash
ibm-lh data-copy --source-data-files <SOURCE_DATA_FILE> --staging-location <STAGING_LOCATION> --staging-s3-creds "AWS_SECRET_ACCESS_KEY=<YOUR_TARGET_SECRET_ASSESS_KEY>,AWS_ACCESS_KEY_ID=<YOUR_TARGET_ACCESS_KEY_ID>,AWS_REGION=<YOUR_TARGET_REGION>, BUCKET_NAME=<YOUR_TARGET_BUCKET>, ENDPOINT_URL=<YOUR_TARGET_ENDPOINT_URL>” --target-tables <TARGET_TABLES> --ingestion-engine-endpoint <INGESTION_ENGINE_ENDPOINT> --dbuser <DBUSER> --dbpassword <DBPASSWORD> --create-if-not-exist
```
{: codeblock}

For example:
```bash
ibm-lh data-copy --source-data-files /cust-bucket/warehouse/a_source_file1.parquet --staging-location s3://cust-bucket/warehouse/staging/ --staging-s3-creds "AWS_ACCESS_KEY_ID=zzzzzz,AWS_SECRET_ACCESS_KEY=vvvvvvv,AWS_REGION=us-east-1,BUCKET_NAME=cust-bucket" --target-tables iceberg_target_catalog.ice_schema.cust_tab1 --ingestion-engine-endpoint "hostname=localhost,port=8080" --create-if-not-exist
```
{: screen}

```bash
ibm-lh data-copy --source-data-files /cust-bucket/warehouse/ --staging-location s3://cust-bucket/warehouse/staging/ --staging-s3-creds "AWS_ACCESS_KEY_ID=zzzzzz,AWS_SECRET_ACCESS_KEY=vvvvvvv,AWS_REGION=us-east-1,BUCKET_NAME=cust-bucket" --target-tables iceberg_target_catalog.ice_schema.cust_tab1 --ingestion-engine-endpoint "hostname=localhost,port=8080" --create-if-not-exist
```
{: screen}
