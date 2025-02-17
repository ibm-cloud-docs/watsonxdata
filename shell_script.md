---

copyright:
  years: 2022, 2024
lastupdated: "2025-02-17"

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

•	-p: DOWNLOAD_DIR (default: /root/data) - The target folder for downloaded files.

•	-x: START_DATE (default: last 24 hours) - The start date for filtering objects.

•	-y: END_DATE (default: current date) - The end date for filtering objects.

•	-h, --base-path - Base path in the bucket.


Example command:

` ./qhmm_usr_export.sh -e <ENDPOINT> -r <REGION> -b <BUCKET_NAME> -a <ACCESS_KEY> -s <SECRET_KEY> -i <WXD_INSTANCE_ID> -t <ENGINE_TYPE> -d <ENGINE_ID> -p <DOWNLOAD_DIR> -x <START_DATE> -y <END_DATE>`

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

` ./qhmm_import_sre.sh -e <ENDPOINT> -r <REGION> -b <BUCKET_NAME> -a <ACCESS_KEY> -s <SECRET_KEY> -i <WXD_INSTANCE_ID> -t <ENGINE_TYPE> -d <ENGINE_ID> -p <COMPRESSED_FILE>`


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
