---

copyright:
  years: 2022, 2024
lastupdated: "2024-09-04"

keywords: watsonxdata, commands, command line interface, cli

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

# Options and parameters supported in **ibm-lh** tool
{: #cli_commands}

Ingesting data files from S3 or local location into {{site.data.keyword.lakehouse_full}} is done by using the **ibm-lh** tool. The parameters that are supported in the **ibm-lh** tool are described in this topic.
{: shortdesc}

## Before you begin:
{: #bybcomndlne}

Set the mandatory environment variable for `ENABLED_INGEST_MODE` before starting an ingestion job. Based on the ingestion mode, specify appropriate value for the variable. Following is an example for Spark.

```bash
export ENABLED_INGEST_MODE=SPARK
```
{: codeblock}

The following ingestion modes are supported:
* `PRESTO`
* `SPARK_LEGACY`
* `SPARK`

SPARK is the default mode.
{: note}

Sample scripts and config file templates are available for CLI ingestion commands in the `/Ingestion-Examples/` folder in the `ibm-lh` tool container. To access the example scripts and config files, run the following command:

1. Run `./ibm-lh data-copy --interactive` to enter the container in interactive mode.
1. Run `cd /Ingestion-Examples/` to access the example scripts and config files.

## Options and parameters
{: #optionsparams}

Different options and variables that are supported in a **ibm-lh** tool that is invoked by `ibm-lh data-copy` command are listed as follows:

|Parameter|Description|Declaration|Modes of ingestion|
|----|----|----|----|
|`create-if-not-exist`|Create target table if it does not exist.|`--create-if-not-exist`|`PRESTO`, `SPARK_LEGACY`, and `SPARK`|
|`dbpassword`|Database password that is used to do ingestion. This is a mandatory parameter to run an ingestion job unless the default user is used.|`--dbpassword <DBPASSWORD>`|`PRESTO`|
|`dbuser`|Database username that is used to do ingestion. This is a mandatory parameter to run an ingestion job unless the default user is used.|`--dbuser <DBUSER>`|`PRESTO`|
|`debug`|Debug the logs of ingestion jobs. The short command for this parameter is `-d`.|`--debug`|`PRESTO`, `SPARK_LEGACY`, and `SPARK`|
|`engine-id`| Engine id of Spark engine when using REST API based `SPARK` ingestion. The short command for this parameter is `-e`.|`--engine-id <spark-enginename>`|`SPARK`|
|`escape-char`| CSV escape property character. Default value is **/**.|`--escape-char <escape_character_value>`|`PRESTO`, `SPARK_LEGACY`, and `SPARK`|
|`encoding`| CSV encoding property character. Default value is `utf-8`.|`--encoding <encoding_value>`|`PRESTO`, `SPARK_LEGACY`, and `SPARK`|
|`field-delimiter`| CSV file field delimiter value. Default value is `,`.|`--field-delimiter <field_delimiter_value>`|`PRESTO`, `SPARK_LEGACY`, and `SPARK`|
|`header`| Mandatory parameter for CSV files with or without a header. Default value is `true`.|`--header <true/false>`|`PRESTO`, `SPARK_LEGACY`, and `SPARK`|
|`ingest-config`|Configuration file for data migration|`--ingest-config <INGEST_CONFIGFILE>`|`PRESTO` and `SPARK_LEGACY`|
|`ingestion-engine-endpoint`|Endpoint of ingestion engine. hostname=`<hostname>`, port=`<port>`. This is a mandatory parameter to run an ingestion job.|`--ingestion-engine-endpoint <INGESTION_ENGINE_ENDPOINT>`|`PRESTO` and `SPARK_LEGACY`|
|`instance-id`|Identify unique instances. In SaaS environment, CRN is the instance id. The short command for this parameter is `-i`.|`--instance-id <instance-CRN>`|`SPARK`|
|`job-id`|Job id is generated when REST API or UI-based ingestion is initiated. This job id is used in getting the status of ingestion job. This parameter is used only with `ibm-lh get-status` command in the interactive mode of ingestion. The short command for this parameter is `-j`.|`ibm-lh get-status --job-id <Job id>`|`SPARK`|
|`all-jobs`|This all-jobs parameter gives the history of all ingestion jobs. This parameter is used only with `ibm-lh get-status` command in the interactive mode of ingestion.|`ibm-lh get-status --all-jobs`|`SPARK`|
|`line-delimiter`| CSV file line delimiter value. Default\n value is`\n` <uicontrol>\n<uicontrol>.|`--line-delimiter <line_delimiter_value>`|`PRESTO`, `SPARK_LEGACY`, and `SPARK`|
|`log-directory`|This option is used to specify the location of log files. See [Log directory](#log_direc).|`--ingest-config <ingest_config_file> --log-directory <directory_path>`|`PRESTO`, `SPARK_LEGACY`, and `SPARK`|
|`partition-by`|Supports the functions for year, month, day, and hour for timestamp in the `partition-by` list. If a target table already exists or the `create-if-not-exist` parameter is not specified, partition-by does not effect the data.|`ibm-lh data-copy --partition-by "<columnname1>, <columnname2>"`|`SPARK_LEGACY` and `SPARK`|
|`password`|Password of the user connecting to the instance. In SaaS, API key of the instance is used. The short command for this parameter is `-pw`.|`--password <apikey>`|`SPARK`|
|`schema`|Schema file that includes CSV specifications, and more. For more details, see [Schema file specifications](#schema_spec).|`--schema </path/to/schemaconfig/file>`|`PRESTO`, `SPARK_LEGACY`, and `SPARK`|
|`source-data-files`|Data files or folders for data migration. File name ending with `/` is considered a folder. Single or multiple files can be used. This is a mandatory parameter to run an ingestion job. Example: `<file1_path>,<file2_path>,<folder1_path>`. File names are case-sensitive. The short command for this parameter is `-s`.|`--source-data-files <SOURCE_DATA_FILE>`|`PRESTO`, `SPARK_LEGACY`, and `SPARK`|
|`staging-location`|Location where CSV files and in some circumstances parquet files are staged, see [Staging location](#stag_loc). This is a mandatory parameter to run an ingestion job.|`--staging-location <STAGING_LOCATION>`|`PRESTO`|
|`staging-hive-catalog`|If the default catalog for staging is not used, use this parameter to specify the name of the Hive catalog that is configured in {{site.data.keyword.lakehouse_short}}. The default catalog is `hive_data`.|`--staging-hive-catalog <catalog_name>`|`PRESTO`|
|`staging-hive-schema`|The schema name associated with the staging hive catalog for ingestion. Create and pass in a custom schema name by using this parameter. Default schema: `lhingest_staging_schema`. If schema is created as default, this parameter is not required.|`--staging-hive-schema <schema_name>`|`PRESTO`|
|`sync-status`|This parameter is used in REST API based ingestion. The default value is `false`. When this parameter is set to `true`, `ibm-lh data-copy` tool waits and polls to get continuous status after an ingestion job is submitted.|`--sync-status <IS THERE ANY ENTRY?>`|`SPARK`|
|`system-config`|This parameter is used to specify system-related parameters. For more information, see [System config](#sys_config).|`--system-config <path/to/system/configfile>`|`PRESTO`, `SPARK_LEGACY`, and `SPARK`|
|`target-catalog-uri`|Target catalog uri|`--target-catalog-uri <TARGET_CATALOG_URI>`|`SPARK_LEGACY`|
|`target-table`|Data migration target table. `<catalog>.<schema>.<table1>`. This is a mandatory parameter to run an ingestion job. Example: `<iceberg.demo.customer1>`. The short command for this parameter is `-t`. For more information, see [Target table](#target_table).|`--target-table <TARGET_TABLE>`|`PRESTO`, `SPARK_LEGACY`, and `SPARK`|
|`trust-store-path`|Path of the truststore to access the ingestion engine. This is used to establish SSL connections. This parameter is mandatory for non-root user.|`--trust-store-path <TRUST_STORE_PATH>`|`PRESTO` and `SPARK_LEGACY`|
|`trust-store-password`|Password of truststore to access the ingestion engine. This is used to establish SSL connections. This parameter is mandatory for non-root user.|`--trust-store-password <TRUST_STORE_PASSWORD>`|`PRESTO` and `SPARK_LEGACY`|
|`user`|Username of the user connecting to the instance. The short command for this parameter is `-u`.|`--user <username>`|`SPARK`|
|`url`|Base url of the location of {{site.data.keyword.lakehouse_full}} cluster. The short command for this parameter is `-w`.|`--url <url>`|`SPARK`|
{: caption="Table 1. Command line options and variables" caption-side="bottom"}

## System config
{: #sys_config}

The `system-config` parameter refers to a file and is used to specify system-related parameters.

For the command line, the parameter is declared as follows:

```bash
--system-config /path/to/systemconfig/file
```
{: codeblock}

The format of the system config parameter is as follows:

```bash
[system-config]
<param_name1>:<param_val>
<param_name2>:<param_val>
<param_name3>:<param_val>
...
```
{: codeblock}

Currently, only the memory-limit parameter is supported. This parameter specifies the maximum memory in watsonx.data that an ingestion job can use. The default value for memory-limit is 500 M. The limit can be in bytes, K, M, or G. The `system-config` is applicable for `PRESTO`, `SPARK_LEGACY`, and `SPARK` ingestion modes.

The following are some examples of how the `memory-limit` parameter can be specified in the system-config file.

```bash
[system-config]
memory-limit:500M

[system-config]
memory-limit:5000K

[system-config]
memory-limit:1G

[system-config]
memory-limit:10000000 #This is in bytes
```
{: codeblock}

The `memory-limit` parameter is applicable for `PRESTO` ingestion mode.
{: note}

## Staging location
{: #stag_loc}

This parameter is applicable for `PRESTO` ingestion mode.

The staging location is used for:
- CSV file or folder ingestion
- Local Parquet file or folder ingestion.
- S3 Parquet file ingestion
- In some circumstances, when the source file or files in the S3 Parquet folder contains special column types, such as TIME or are associated with different column types.

For ingestion job through CLI, the staging bucket must be the same bucket that is associated with the Hive catalog. Staging is possible only in the Hive catalog.
{: important}

The internal MinIO buckets (iceberg-data, hive-data, wxd-milvus, wxd-system) and their associated catalogs cannot be used for staging, as their endpoints are not externally accessible. Users can use their own storage buckets that are exposed and accessible by external connections.
{: note}

## Schema file specification
{: #schema_spec}

The schema parameter points to the schema file. The schema file can be used to specify CSV file properties such as field delimiter, line delimiter, escape character, encoding and whether header exists in the CSV file. This parameter is applicable for `PRESTO`, `SPARK_LEGACY`, and `SPARK` ingestion modes.

The following is the schema file specification:

```bash
[CSV]
DELIMITER:<delim> #default ','

#LINE_DELIMITER:
#A single char delimiter other than ' '(blank), need not be enclosed in quotes.
#Must be enclosed in quotes if it is one of:  '\n' for newline, '\t' for TAB, ' ' for space.
LINE_DELIMITER:<line_delim> #default '\n'

HEADER:<true|false> #default 'true'
#HEADER is a mandatory entry within schema file.

#single character value
ESCAPECHAR:<escape_char>   #default '\\'

#Encoding (Example:"utf-8")
ENCODING:<encoding>    #default None
```
{: codeblock}

The encodings supported by Presto and Spark ingestion are directly dependent on encodings supported by [Python](https://docs.python.org/3/library/codecs.html#standard-encodings). The encoding value must be enclosed in double quotation marks.
{: note}

The following is an example of schema specification:

```bash
$ more /tmp/schema.cfg
[CSV]
DELIMITER:','
HEADER:false
LINE_DELIMITER:'\n'
```
{: screen}

## Log directory
{: #log_direc}

The ingest log files are generated in the log directory. By default, the ingest log file is generated as `/tmp/ingest.log`. By using the `--log-directory` parameter, you can specify a new location for ingest log files. A separate log file is created for each ingest command invocation. The new log file name is in the format `ingest_<timestamp)_<pid>.log`. The log directory must exist before invocation of the **ibm-lh** ingest tool.

This parameter is applicable only in the command-line option for `PRESTO`, `SPARK_LEGACY`, and `SPARK` ingestion modes.

Example when using the command line:

```bash
ibm-lh data-copy --source-data-files s3://cust-bucket/warehouse/a_source_file1.csv,s3://cust-bucket/warehouse/a_source_file2.csv
--staging-location s3://cust-bucket/warehouse/staging/
--target-table iceberg_target_catalog.ice_schema.cust_tab1
--ingestion-engine-endpoint "hostname=localhost,port=8080"
--create-if-not-exist
--log-directory /tmp/mylogs
```
{: codeblock}

Example when using a config file:

```bash
ibm-lh data-copy --ingest-config ext.cfg --log-directory /tmp/mylogs
```
{: codeblock}

## Target table
{: #target_table}

The ability to handle special characters in table and schema names for ingestion is constrained by the underlying engines (Presto, Legacy Spark, Spark) and the special characters they support. When using schema or table names with special characters, not all special characters are accepted by Spark, Presto, Legacy Spark. Consult the documentation for the special characters support.

The SQL identifier of the target table for data migration is `<catalog>.<schema>.<table>`. Use double quotation marks " or backticks ` to escape parts with special characters.

Examples:

```bash
`ibm-lh data-copy --target-table 'catalog."schema 2.0"."my table!"'`
{: codeblock}

```bash
ibm-lh data-copy --target-table 'catalog.`schema 2.0`.`my table!`'
```
{: codeblock}

```bash
`ibm-lh data-copy --target-table catalog.'"schema 2.0"'.'"my table!"'`
{: codeblock}

```bash
ibm-lh data-copy --target-table "catalog.\`schema 2.0\`.\`my table!\`"
```
{: codeblock}

```bash
`ibm-lh data-copy --target-table catalog.\"schema\ 2.0\".\"my\ table!\"`
{: codeblock}

Both double quotation marks " and backticks ` are accepted, but quotation mark styles cannot be mixed. In order to include a literal quotation inside an identifier, double the quoting character (for example, "" or ``).
{: note}
