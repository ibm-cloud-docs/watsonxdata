---

copyright:
  years: 2022, 2023
lastupdated: "2023-07-07"

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

Ingesting data files from S3 or local location into {{site.data.keyword.lakehouse_full}} is done by using two options that are supported in **ibm-lh** tool.
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
   |source-data-files|Data file(s) or folder(s) for data migration. File name ending with `/` is considered a folder. Single or multiple files can be used. Example: `<file1_path>,<file2_path>,<folder1_path>`|`ibm-lh data-copy --source-data-files <SOURCE_DATA_FILE>`
   |source-s3-creds|S3 credentials of data source|`ibm-lh data-copy --source-s3-creds <SOURCE_S3_CREDS>`|
   |staging-location|Location where CSV files are converted to Parquet are staged. Even parquet files in some circumstances are staged like, Parquet file is local, Parquet files in local folder, a huge Parquet file(local or S3) all of which may not fit in memory, source file is S3 parquet file, and file from S3 parquet folder which may contain special column types such as date or decimal. Example: `<s3://lh-target/staging>`|`ibm-lh data-copy --staging-location <STAGING_LOCATION>`|
   |staging-s3-creds|S3 credentials of staging location|`ibm-lh data-copy --staging-s3-creds <STAGING_S3_CREDS>`|
   |staging-hive-catalog|If the default hive catalog cannot be used due to credential mismatch with source or staging locations, it is possible to configure a custom hive catalog using this option|`ibm-lh data-copy --staging-hive-catalog <catalog_name>`|
   |system-config|This parameter can be used to specify system related parameters such as memory limit|`ibm-lh data-copy --system-config <file_path>`|
   |log-directory|This option is used to specify the location of log files. The ingest log files will be created undeneath the given directory. Default ingest log file is `/tmp/ingest.log`|`ibm-lh data-copy --ingest-config <ingest_config_file> --log-directory <directory_path>`|
   |target-catalog-uri|Target catalog uri|`ibm-lh data-copy --target-catalog-uri <TARGET_CATALOG_URI>`|
   |target-table-storage|Target table file storage location|`ibm-lh data-copy --target-table-storage <TARGET_TABLE_STORAGE>`|
   |target-tables|Data migration target table. `<catalog>.<schema>.<table1>`. Example: `<iceberg.demo.customer1>`|`ibm-lh data-copy --target-tables <TARGET_TABLES>`|
   |schema|Schema file that includes CSV specifications, and so on|`ibm-lh data-copy --schema <SCHEMA>`|
   |target-s3-creds|S3 credentials of target location|`ibm-lh data-copy --target-s3-creds <TARGET_S3_CREDS>`|
   |ingestion-engine-endpoint|Endpoint of ingestion engine. hostname=`<hostname>`,port=`<port>`|`ibm-lh data-copy --ingestion-engine-endpoint <INGESTION_ENGINE_ENDPOINT>`|
   |dbuser|Username of ingestion engine|`ibm-lh data-copy --dbuser <DBUSER>`|
   |dbpassword|User password of ingestion engine|`ibm-lh data-copy --dbpassword <DBPASSWORD>`
   |trust-store-path|Path of truststore to access ingestion engine. This is used for making SSL connections.|`ibm-lh data-copy --trust-store-path <TRUST_STORE_PATH>`|
   |trust-store-password|Password of truststore to access ingestion engine. This is used for making SSL connections.|`ibm-lh data-copy --trust-store-password <TRUST_STORE_PASSWORD>`|
   |create-if-not-exist|Create target table if not existed|`ibm-lh data-copy --create-if-not-exist`|
   {: caption="Table 1. Command line options and variables" caption-side="bottom"}

1. **Configuration file** option

   The **Configuration file** contains a global ingest configuration section and multiple individual ingest configuration sections to perform the ingestion job. The specifications of the individual ingestion sections override the specifications of the global ingestion section.

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
   |source-files|Data file(s) or folder(s) for data migration. File name ending with `/` is considered a folder|`source-files:<SOURCE_DATA_FILE>`
   |source-s3-creds|S3 credentials of data source|`source-s3-creds:<SOURCE_S3_CREDS>`|
   |staging-location|Location where CSV files are converted to Parquet are staged. Even parquet files in some circumstances are staged like, Parquet file is local, Parquet files in local folder, a huge Parquet file(local or S3) all of which may not fit in memory, source file is S3 parquet file, and file from S3 parquet folder which may contain special column types such as date or decimal. Example: `<s3://lh-target/staging>`|`staging-location:<STAGING_LOCATION>`|
   |staging-s3-creds|S3 credentials of staging location|`source-s3-creds:<SOURCE_S3_CREDS>`|
   |staging-hive-catalog|If the default hive catalog cannot be used due to credential mismatch with source or staging locations, it is possible to configure a custom hive catalog using this option|`staging-hive-catalog:<catalog_name>`|
   |system-config|This parameter can be used to specify system related parameters such as memory limit|`system-config:<file_path>`|
   |target-catalog-uri|Target catalog uri|`target-catalog-uri:<TARGET_CATALOG_URI>`|
   |target-table-storage|Target table file storage location|`target-table-storage:<TARGET_TABLE_STORAGE>`|
   |target-tables|Data migration target table. `<catalog>.<schema>.<table1>`. Example: `<iceberg.demo.customer1>`|`target-tables:<TARGET_TABLES>`|
   |schema|Schema file that includes CSV specifications, and so on|`schema:<SCHEMA>`|
   |target-s3-creds|S3 credentials of target location|`target-s3-creds:<TARGET_S3_CREDS>`|
   |ingestion-engine-endpoint|Endpoint of ingestion engine. hostname=`<hostname>`,port=`<port>`|`ingestion-engine-endpoint:<INGESTION_ENGINE_ENDPOINT>`|
   |dbuser|Username of ingestion engine|`dbuser:<DBUSER>`|
   |dbpassword|User password of ingestion engine|`dbpassword:<DBPASSWORD>`|
   |trust-store-path|Path of truststore to access ingestion engine|`trust-store-path:<TRUST_STORE_PATH>`|
   |trust-store-password|Password of truststore to access ingestion engine|`trust-store-password:<TRUST_STORE_PASSWORD>`|
   |create-if-not-exist|Create target table if not existed|`create-if-not-exist`|
   {: caption="Table 3. Individual ingest config options and variables" caption-side="bottom"}

## Schema file specification
{: #schema_spec}

The schema parameter points to the schema file. The schema file can be used to specify CSV file properties such as field delimiter, line delimiter, escape character, encoding and whether header exists in CSV file.

Following is the schema file specification:

```bash
[CSV]
DELIMITER:<delim> #default '|'

#LINE_DELIMITER:
#A single char delimiter other than ' '(blank), need not be enclosed in quotes
#Must be enclosed in quotes if it is one of:  '\n' for newline, '\t' for TAB, ' ' for space
LINE_DELIMITER:<line_delim> #default '\n'

HEADER:<true|false> #default 'true'

#single character value
ESCAPECHAR:<escape_char>   #default '\\'

#Example encodings:
#utf-8, cp1252, iso-88509-1, latin1 etc
ENCODING:<encoding>    #default None
```
{: codeblock}

Following is an example of schema specification:

Example:
```bash
$ more /tmp/schema.cfg
[CSV]
DELIMITER:,
HEADER:false
LINE_DELIMITER:'\n'
```
{: screen}
