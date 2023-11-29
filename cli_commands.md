---

copyright:
  years: 2022, 2023
lastupdated: "2023-11-29"

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

Ingesting data files from S3 or local location into {{site.data.keyword.lakehouse_full}} is done by using two options that are supported in the **ibm-lh** tool.
{: shortdesc}

1. **Command line** option

1. **Configuration file** option

   a. Global ingest config section

   b. Individual ingest config section

Different options and variables that are supported in a command line and configuration file are listed as follows:

1. **Command line** option

   |Parameter|Description|Declaration|
   |----|----|----|
   |generate-ddl|Generate schema for parquet data file|`ibm-lh data-copy --generate-ddl`
   |ingest-config|Configuration file for data migration|`ibm-lh data-copy --ingest-config <INGEST_CONFIGFILE>`
   |source-data-files|Data files or folders for data migration. File name ending with `/` is considered a folder. Single or multiple files can be used. This is a mandatory parameter to run ingestion job. Example: `<file1_path>,<file2_path>,<folder1_path>`|`ibm-lh data-copy --source-data-files <SOURCE_DATA_FILE>`
   |source-s3-creds|S3 credentials of data source|`ibm-lh data-copy --source-s3-creds <SOURCE_S3_CREDS>`|
   |staging-location|Location where CSV files and in some circumstances parquet files are staged, see [Staging location](#stag_loc). This is a mandatory parameter to run ingestion job.|`ibm-lh data-copy --staging-location <STAGING_LOCATION>`|
   |staging-s3-creds|S3 credentials of staging location. This is a mandatory parameter to run ingestion job.|`ibm-lh data-copy --staging-s3-creds <STAGING_S3_CREDS>`|
   |staging-hive-catalog|The hive catalog name configured in the watsonx.data, if not using the default catalog for staging. Default catalog: hive_data.|`ibm-lh data-copy --staging-hive-catalog <catalog_name>`|
   |staging-hive-schema|The schema name associated with the staging hive catalog for ingestion. A default schema must be created by the users in their staging catalog, or create and pass in a custom schema name by using this parameter. Default schema: lhingest_staging_schema.|`ibm-lh data-copy --staging-hive-schema <schema_name>`|
   |system-config|This parameter is used to specify system related parameters.|`ibm-lh data-copy --system-config <path/to/system/configfile>`|
   |log-directory|This option is used to specify the location of log files. See [Log directory](#log_direc).|`ibm-lh data-copy --ingest-config <ingest_config_file> --log-directory <directory_path>`|
   |target-catalog-uri|Target catalog uri|`ibm-lh data-copy --target-catalog-uri <TARGET_CATALOG_URI>`|
   |target-table-storage|Target table file storage location|`ibm-lh data-copy --target-table-storage <TARGET_TABLE_STORAGE>`|
   |target-tables|Data migration target table. `<catalog>.<schema>.<table1>`. This is a mandatory parameter to run ingestion job. Example: `<iceberg.demo.customer1>`|`ibm-lh data-copy --target-tables <TARGET_TABLES>`|
   |schema|Schema file that includes CSV specifications, and more. This is a mandatory parameter to run ingestion job, if source file is CSV. See [Schema file specifications](#schema_spec).|`ibm-lh data-copy --schema </path/to/schemaconfig/file>`|
   |target-s3-creds|S3 credentials of target location|`ibm-lh data-copy --target-s3-creds <TARGET_S3_CREDS>`|
   |ingestion-engine-endpoint|Endpoint of ingestion engine. hostname=`<hostname>`,port=`<port>`. This is a mandatory parameter to run ingestion job.|`ibm-lh data-copy --ingestion-engine-endpoint <INGESTION_ENGINE_ENDPOINT>`|
   |dbuser|Database username that is used to do ingestion. This is a mandatory parameter to run ingestion job unless the default user is used.|`ibm-lh data-copy --dbuser <DBUSER>`|
   |dbpassword|Database password that is used to do ingestion. This is a mandatory parameter to run ingestion job unless the default user is used.|`ibm-lh data-copy --dbpassword <DBPASSWORD>`
   |trust-store-path|Path of truststore to access ingestion engine. This is used for making SSL connections. This is a mandatory parameter to run ingestion job.|`ibm-lh data-copy --trust-store-path <TRUST_STORE_PATH>`|
   |trust-store-password|Password of truststore to access the ingestion engine. This is used for making SSL connections. This is a mandatory parameter to run ingestion job.|`ibm-lh data-copy --trust-store-password <TRUST_STORE_PASSWORD>`|
   |create-if-not-exist|Create target table if not existed|`ibm-lh data-copy --create-if-not-exist`|
   {: caption="Table 1. Command line options and variables" caption-side="bottom"}

1. **Configuration file** option

   The **Configuration file** contains a global ingest configuration section and multiple individual ingest configuration sections to run the ingestion job. The specifications of the individual ingestion sections override the specifications of the global ingestion section.

   a. Global ingest config section

   |Parameter|Description|Declaration|
   |----|----|----|
   |target-tables|Data migration target table. One target table can only be specified. `<catalog>.<schema>.<table1>`|`target-tables:<table_name>`|
   |ingestion-engine-endpoint|Specifies connection parameters of the ingestion engine. Endpoint of ingestion engine. hostname=`<hostname>`,port=`<port>`|`ingestion-engine:hostname=<hostname>, port=<port>`|
   |create-if-not-exist|Create target table if not existed|`create-if-not-exist:<true|false>`|
   {: caption="Table 2. Global ingest config options and variables" caption-side="bottom"}

   b. Individual ingest config section

   There can be multiple individual ingest sections in a configuration file option. Each individual ingest config sections will be ingested separately.
   {: note}

   |Parameter|Description|Declaration|
   |----|----|----|
   |source-files|Data files or folders for data migration. File name ending with `/` is considered a folder. This is a mandatory parameter to run ingestion job.|`source-files:<SOURCE_DATA_FILE>`
   |source-s3-creds|S3 credentials of data source.|`source-s3-creds:<SOURCE_S3_CREDS>`|
   |staging-location|Location where CSV files and in some circumstances parquet files are staged, see [Staging location](#stag_loc). This is a mandatory parameter to run ingestion job.|`staging-location:<STAGING_LOCATION>`|
   |staging-s3-creds|S3 credentials of staging location. This is a mandatory parameter to run ingestion job.	source-s3-creds:<SOURCE_S3_CREDS>|`source-s3-creds:<SOURCE_S3_CREDS>`|
   |staging-hive-catalog|The hive catalog name configured in the watsonx.data, if not using the default catalog for staging. Default catalog: hive_data.|`ibm-lh data-copy --staging-hive-catalog <catalog_name>`|
   |staging-hive-schema|The schema name associated with the staging hive catalog for ingestion. A default schema must be created by the users in their staging catalog, or create and pass in a custom schema name by using this parameter. Default schema: lhingest_staging_schema.|`ibm-lh data-copy --staging-hive-schema <schema_name>`|
   |system-config|This parameter is used to specify system related parameters.|`ibm-lh data-copy --system-config <path/to/system/configfile>`|
   |target-catalog-uri|Target catalog uri|`target-catalog-uri:<TARGET_CATALOG_URI>`|
   |target-table-storage|Target table file storage location|`target-table-storage:<TARGET_TABLE_STORAGE>`|
   |target-tables|Data migration target table. `<catalog>.<schema>.<table1>`. This is a mandatory parameter to run ingestion job. Example: `<iceberg.demo.customer1>`|`target-tables:<TARGET_TABLES>`|
   |schema|Schema file that includes CSV specifications, and more. This is a mandatory parameter to run ingestion job, if source file is CSV. See [Schema file specifications](#schema_spec)|`schema:/path/to/schemaconfig/file`|
   |target-s3-creds|S3 credentials of target location|`target-s3-creds:<TARGET_S3_CREDS>`|
   |ingestion-engine-endpoint|Endpoint of ingestion engine. hostname=`<hostname>`,port=`<port>`. This is a mandatory parameter to run ingestion job.|`ingestion-engine-endpoint:<INGESTION_ENGINE_ENDPOINT>`|
   |dbuser|Database username that is used to do ingestion. This is a mandatory parameter to run ingestion job unless the default user is used.|`dbuser:<DBUSER>`|
   |dbpassword|Database password that is used to do ingestion. This is a mandatory parameter to run ingestion job unless the default user is used.|`dbpassword:<DBPASSWORD>`|
   |trust-store-path|Path of truststore to access ingestion engine. This is used for making SSL connections. This is a mandatory parameter to run ingestion job.|`trust-store-path:<TRUST_STORE_PATH>`|
   |trust-store-password|Password of truststore to access the ingestion engine. This is used for making SSL connections. This is a mandatory parameter to run ingestion job.|`trust-store-password:<TRUST_STORE_PASSWORD>`|
   |create-if-not-exist|Create target table if not existed|`create-if-not-exist`|
   {: caption="Table 3. Individual ingest config options and variables" caption-side="bottom"}

## Staging location
{: #stag_loc}

The staging location is used for:
- CSV file or folder ingestion
- Local Parquet file or folder ingestion.
- S3 Parquet file ingestion
- In some circumstances, when the source file in a S3 Parquet folder contains special column types, such as DATE or DECIMAL.

For ingestion job through CLI, the staging bucket must be the same bucket that is associated with the Hive catalog. Staging is possible only in the Hive catalog.
{: important}

## Schema file specification
{: #schema_spec}

The schema parameter points to the schema file. The schema file can be used to specify CSV file properties such as field delimiter, line delimiter, escape character, encoding and whether header exists in CSV file.

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

#Example encodings:
#utf-8, cp1252, iso-88509-1, latin1 etc
ENCODING:<encoding>    #default None
```
{: codeblock}

The following is an example of schema specification:

```bash
$ more /tmp/schema.cfg
[CSV]
DELIMITER:,
HEADER:false
LINE_DELIMITER:'\n'
```
{: screen}

## Log directory
{: #log_direc}

The ingest log files are generated in the log directory. By default, the ingest log file is generated as `/tmp/ingest.log`. By using the `--log-directory` parameter, you can specify a new location for ingest log files. A separate log file is created for each ingest command invocation. The new log file name is in the format `ingest_<timestamp)_<pid>.log`. The log directory must exist before invocation of the **ibm-lh** ingest tool.

This parameter is applicable only in the command line option.

Example by using command line:

```bash
ibm-lh data-copy --source-data-files s3://cust-bucket/warehouse/a_source_file1.csv,s3://cust-bucket/warehouse/a_source_file2.csv
--source-s3-creds "AWS_ACCESS_KEY_ID=xxxxxx,AWS_SECRET_ACCESS_KEY=yyyyyy,AWS_REGION=us-east-1,BUCKET_NAME=cust-bucket"
--staging-location s3://cust-bucket/warehouse/staging/
--staging-s3-creds "AWS_ACCESS_KEY_ID=zzzzzz,AWS_SECRET_ACCESS_KEY=vvvvvvv,AWS_REGION=us-east-1,BUCKET_NAME=cust-bucket"
--target-tables iceberg_target_catalog.ice_schema.cust_tab1
--ingestion-engine-endpoint "hostname=localhost,port=8080"
--create-if-not-exist
--log-directory /tmp/mylogs
```
{: codeblock}

Example with a config file:

```bash
ibm-lh data-copy --ingest-config ext.cfg --log-directory /tmp/mylogs
```
{: codeblock}
