---

copyright:
  years: 2022, 2025
lastupdated: "2025-03-24"

keywords: watsonxdata, qhmm

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

# QHMM Shell Script usage
{: #qhmm_shell}

This topic provides instructions on using two shell scripts, `qhmm_usr_export.sh` and `qhmm_import_sre.sh`, for diagnostic data handling in QHMM.

## Prerequisites
{: #qhmm_shell-preq}

The administrator must get the QHMM Shell Script from IBM Support team.


## qhmm_usr_export.sh
{: #script01}

This script allows users to bundle diagnostic data files from their QHMM diagnostic bucket and share the compressed diagnostic file with support team for further analysis. (This can be done by uploading them to an Enhanced Customer Data Repository (ECuRep)). The script accepts command-line arguments for configuration or can be run with default values.

•	-e: ENDPOINT (default: none) - The storage endpoint.

•	-r: REGION (default: none) - The storage region.

•	-b: BUCKET_NAME (default: none) - The name of the bucket.

•	-a: ACCESS_KEY (default: none) - The access key for the storage.

•	-s: SECRET_KEY (default: none) - The secret key for the storage.

•	-i: WXD_INSTANCE_ID (default: none) - The instance ID of WXD.

•	-t: ENGINE_TYPE (default: none) - The type of the engine (e.g., Presto).

•	-d: ENGINE_ID (default: none) - The ID of the engine.

•	--data-type - The data to be exported (support Dump, QueryEvent, and QueryHistory).

•	-p: DOWNLOAD_DIR (default: /root/data) - The target folder for downloaded files.

•	-x: START_DATE (default: last 24 hours) - The start date for filtering objects.

•	-y: END_DATE (default: current date) - The end date for filtering objects.

•	-h, --base-path - Base path in the bucket.


Example command:

```bash
./qhmm_usr_export.sh -e <ENDPOINT> -r <REGION> -b <BUCKET_NAME> -a <ACCESS_KEY> -s <SECRET_KEY> -i <WXD_INSTANCE_ID> -t <ENGINE_TYPE> -d <ENGINE_ID> -p <DOWNLOAD_DIR> -x <START_DATE> -y <END_DATE>
```
{: codeblock}

## qhmm_import_sre.sh
{: #script02}

This script is intended for the support team to retrieve diagnostic data from an Enhanced Customer Data Repository (ECuRep), and upload it to a support team bucket for further analysis. Similar to the first script, it can be configured using command-line arguments or run with default values.

•	-e: ENDPOINT (default: none) - The storage endpoint.

•	-r: REGION (default: none) - The storage region.

•	-b: BUCKET_NAME (default: none) - The name of the bucket.

•	-a: ACCESS_KEY (default: none) - The access key for the storage.

•	-s: SECRET_KEY (default: none) - The secret key for the storage.

•	-i: WXD_INSTANCE_ID (default: none) - The instance ID of WXD.

•	-t: ENGINE_TYPE (default: none) - The type of the engine (e.g., Presto).

•	-d: ENGINE_ID (default: none) - The ID of the engine.

•	-p: COMPRESSED_FILE (default: /root/data/bundle.zip) - The source folder for the compressed file.


Example command:

```bash
./qhmm_import_sre.sh -e <ENDPOINT> -r <REGION> -b <BUCKET_NAME> -a <ACCESS_KEY> -s <SECRET_KEY> -i <WXD_INSTANCE_ID> -t <ENGINE_TYPE> -d <ENGINE_ID> -p <COMPRESSED_FILE>
```
{: codeblock}

## bucket_data_migration.sh
{: #script03}

This script allows users to transfer QHMM data from the source bucket to the destination bucket. The migration script can be configured by using the following command-line arguments or run with default values:

•	-se: --source-endpoint - Endpoint URL of the source S3-compatible storage (default: http://localhost:9000)

•	-se: --source-endpoint - Endpoint URL of the source S3-compatible storage (default: http://localhost:9000)

• -sr: --source-region - Region of the source S3-compatible storage (default: us-east-1)

• -sb: --source-bucket - Name of the source bucket (required)

• -sa: --source-access-key - Access key for source storage (required)

• -ss: --source-secret-key - Secret key for source storage (required)

• -sbp: --source-base-path - Base path in the source bucket (default: qhmm)

• -de: --dest-endpoint - Endpoint URL of the destination S3-compatible storage (default: http://localhost:9000)

• -dr: --dest-region - Region of the destination S3-compatible storage (default: us-east-1)

• -db: --dest-bucket - Name of the destination bucket (required)

• -da: --dest-access-key - Access key for destination storage (required)

• -ds: --dest-secret-key - Secret key for destination storage (required)

• -dbp: --dest-base-path - Base path in the destination bucket (default: qhmm)

• -bp: --base-path - Base path in the bucket (default: qhmm)

• -i: --instance-id - Instance ID (required)

• -t: --engine-type - Engine type (required)

• -d: --engine-id - Engine ID (required)

• -x: --start-date - Start date for filtering objects (DD-MM-YYYY, optional)

• -y: --end-date - End date for filtering objects (DD-MM-YYYY, optional)

• --data-type - Data to be exported (supported types: Dump, QueryEvent, QueryHistory, optional)

• --max-size - Maximum download size in MB (default: 500MB)

• --help - Display this help and exit

Example command:

```bash
./bucket_data_migration.sh \
    --source-endpoint <source-endpoint> \
    --source-bucket <source-bucket> \
    --source-access-key <source-access-key> \
    --source-secret-key <source-secret-key> \
    --source-base-path <source-base-path> \
    --dest-endpoint <dest-endpoint> \
    --dest-bucket <dest-bucket> \
    --dest-access-key <dest-access-key> \
    --dest-secret-key <dest-secret-key> \
    --dest-base-path <dest-base-path> \
    --instance-id <instance-id> \
    --engine-type <engine-type> \
    --engine-id <engine-id> \
    --start-date <start-date> \
    --end-date <end-date> \
    --data-type <data-type> \
    --max-size <max-size>
```
{: codeblock}

## Managing diagnostic data by manual method
{: #mnl_mthod}

1.	Run the following command to create a table to store the query event data generated using `qhmm_import_sre.sh`:


``` bash
` CREATE TABLE IF NOT EXISTS <catalog>.diag.query_event_raw (
  record VARCHAR,
  dt VARCHAR
)
WITH (
  external_location = 's3a://<bucket>/qhmm/<instance-id>/<engine>/<engine-id>/QueryEvent/',
  format = 'textfile',
  partitioned_by = ARRAY['dt']
);`
```
{: codeblock}

2.	Run the following command to create a table to store the query history data in JSON format:

``` bash
` CREATE TABLE IF NOT EXISTS <catalog>.diag.query_history(
  query_id VARCHAR,
  query VARCHAR,
  state VARCHAR,
  source VARCHAR,
  created VARCHAR,
  started VARCHAR,
  "end" VARCHAR,
  dt VARCHAR,
  user VARCHAR)
WITH (
  external_location = 's3a://<bucket>/qhmm/<instance-id>/<engine>/<engine-id>/QueryHistory/',
  format = 'JSON',
  partitioned_by = ARRAY['dt','user']
);`
```
{: codeblock}

3.	For instructions on diagnosing data in QHMM, follow instructions in [Managing diagnostic data by manual method]({{site.data.keyword.ref-mon_mng-link}}).
