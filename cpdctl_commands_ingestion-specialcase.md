---

copyright:
  years: 2022, 2025
lastupdated: "2025-09-23"

keywords: lakehouse, database, tags, description, watsonx.data

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
{:attention: .attention}
{:remember: .remember}
{:deprecated: .deprecated}
{:pre: .pre}
{:video: .video}

# Additional Information about `ingestion` command usage and special cases
{: #cpdctl_commands_ingestion-specialcase}

This topic provides guidance on using the `cpdctl wx-data ingestion create` command for various ingestion scenarios, including folder ingestion, adhoc ingestion, and ingestion from databases or snapshots. It highlights special cases, edge conditions, and practical examples to help users perform data ingestion effectively.

   All the examples in this topic are referenced based on the examples you get using the help command explained in the "How to use wx-data command --help (-h)" section.
   {: attention}

## Scenario 1: Basic ingestion examples
{: #cpdctl_commands_ingestion-specialcase1}

The following are some examples of basic ingestion commands:

1. Ingestion with registered storage with Spark engine

   ```bash
   ./cpdctl wx-data ingestion create  \
   --source-data-files s3://bucketcos/titanic-parquet.txt \
   --engine-id spark690 \
   --target-table iceberg_data.schema1.cli_table5
   ```
   {: screen}

1. Lite ingestion with registered storage

   ```bash
   ./cpdctl wx-data ingestion create  \
   --source-data-files s3://bucketcos/jsonFile.json \
   --engine-id lite-ingestion \
   --target-table iceberg_data.schema1.cli_table2
   ```
   {: screen}

1. Ingestion with registered database with Spark engine

   ```bash
   ./cpdctl wx-data ingestion create  \
   --database-id postgresql241 \
   --database-schema Tm_Lh_Engine \
   --database-table admission \
   --engine-id spark66 \
   --target-table iceberg_data.schema1.cli_table6 \
   --sync-status
   ```
   {: screen}

## Scenario 2: Folder ingestion
{: #cpdctl_commands_ingestionspecialcase2}

- **Supported engine**: Folder ingestion is only supported by the **Spark** engine.
- **Required parameter**: Users must specify the `--source-file-type` when ingesting from a folder.

   Example:

   ```bash
   cpdctl wx-data ingestion create --source-data-files s3://bucketcos/csv_folder --source-file-type csv
   --target-table iceberg_data.cpdctl_test.test1
   --engine-id spark66
   --job-id cli-test2
   ```
   {: screen}

## Scenario 3: Adhoc ingestion (without registered storage)
{: #cpdctl_commands_ingestionspecialcase3}

Users can perform ingestion without registering storages by providing credentials directly through CLI parameters.

S3 and ADLS storage credentials can be given using `--storage-details` argument or the corresponding independent arguments.

1. Ingestion using S3 storage

Example using `--storage-details`:

   ```bash
   cpdctl wx-data ingestion create --source-data-files s3://bucketcos/titanic-parquet.txt
   --storage-details '{"secret_key":"*****","endpoint":"https://s3.us-west.cloud-object-storage.test.appdomain.cloud","type":"ibm_cos", "access_key":"*****","name":"bucketcos", "region":"us-south"}'
   --engine-id lite-ingestion
   --target-table    iceberg_data.schema1.cli_table1
   ```
   {: screen}

Example using individual storage arguments:

   ```bash
   cpdctl wx-data ingestion create
   --source-data-files    s3://bucketcos/userdata5.avro
   --storage-access-key ******
   --storage-endpoint https://s3.us-west.cloud-object-storage.test.appdomain.cloud
   --storage-name bucketcos
   --storage-region us-south
   --storage-secret-key ******
   --storage-type ibm_cos
   --engine-id lite-ingestion
   --target-table iceberg_data.schema1.cli_table1 --target-write-mode overwrite
   ```
   {: screen}

1. Ingestion using ADLS gen1 storage

Example:

   ```bash
   cpdctl wx-data ingestion create  \
   --source-data-files wasbs://lhcasblob2@lhcastest2.blob.core.windows.net/ingest_data_folder/employees_new_comma.orc \
   --storage-details '{"name":"lhcasblob2-lhcastest2", "endpoint":"wasbs://lhcasblob2@lhcastest2.blob.core.windows.net", "type":"adls_gen1", "access_key":"*******", "container_name":"lhcasblob2", "account_name":"lhcastest2"}' \
   --engine-id lite-ingestion \
   --target-table iceberg_data.schema1.cli_table3
   ```
   {: screen}

1. Ingestion using ADLS gen2 storage

Example:

   ```bash
   cpdctl wx-data ingestion create  \
   --source-data-files abfss://pyspark@sparkadlsiae.dfs.core.windows.net/ingest_data_folder/iris.parquet \
   --storage-details '{"name":"pyspark-sparkadlsiae", "endpoint":"abfss://pyspark@sparkadlsiae.dfs.core.windows.net", "type":"adls_gen2", "application_id":"*****", "directory_id":"*****", "secret_key":"*******", "container_name":"pyspark", "account_name":"sparkadlsiae"}' \
   --engine-id spark66 \
   --target-table iceberg_data.schema1.cli_table4 \
   --sync-status
   ```
   {: screen}

1. Ingestion using database source

Users can ingest data from databases either by using registered database IDs or by providing connection details directly.

Example with direct connection details:

   ```bash
   cpdctl wx-data ingestion create  \
   --engine-id spark66 \
   --database-type netezza \
   --database-name conopsdb \
   --database-host 9.46.64.138 \
   --database-isssl=true \
   --database-port 5480 \
   --database-user-id **** \
   --database-password ***** \
   --database-schema TM_LAKEHOUSE_ENGINE \
   --database-table STUDENTS \
   --database-certificate "$(cat /Useshibilrahmanp/Documents/db_certs/netezpem)" \
   --target-table iceberg_data.schemcli_table10 \
   --target-write-mode overwrite \
   --sync-status
   ```
   {: screen}

   - `--database-certificate` accepts the certificate as a string. To use a file path, use command: `--database-certificate "$(cat </path/to/certificate.pem>)"`.
   - `--database-isssl=true` is required for SSL-enabled databases and must provide certificate using the parameter `--database-certificate`.
   - For **Oracle**, `--database-connection-mode` (either `sid` or `service_name`) and `--database-connection-mode-value` parameters are required.

## Scenario 4: Ingestion using Iceberg `snapshot-id` with Spark engine
{: #cpdctl_commands_ingestion-specialcase4}

Example:

   ```bash
   cpdctl wx-data ingestion create --instance-id 1735472262311515 --iceberg-catalog sample_iceberg_catalog    --iceberg-schema sample_iceberg_schema --iceberg-snapshot-id 7823318841638214979 --iceberg-table sample_iceberg_table    --iceberg-warehouse sample_iceberg_warehouse --target-table sample_catalog.sample_schema.sample_table --engine-id    spark266 --storage-name iceberg-data
   ```
   {: screen}


## Additional Help
{: #cpdctl_commands_ingestion-specialcase5}

To explore more options and flags supported by the `ingestion` command, run the following:

   ```bash
   cpdctl wx-data ingestion create --help
   ```
   {: codeblock}
