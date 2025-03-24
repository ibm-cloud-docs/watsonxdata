---

copyright:
  years: 2022, 2025
lastupdated: "2025-03-24"

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

# Presto ingestion using **ibm-lh** utility through CLI
{: #ingest_presto_cli}

You can ingest data from an S3 or local location into {{site.data.keyword.lakehouse_full}} using the **ibm-lh** utility. The following options are supported:

* **Command line** option
* **Configuration file** option
{: shortdesc}

This topic provides details about the parameters supported in **ibm-lh** utility for ingestion using Presto engine. For detailed instructions to ingest, see:

* [Ingesting data through command line - Presto ingestion mode](/docs/watsonxdata?topic=watsonxdata-ingest_datafiles_cli)
* [Ingesting data through config file - Presto ingestion mode](/docs/watsonxdata?topic=watsonxdata-ingest_datafiles_config)

Different options and variables that are supported in a command line and configuration file are listed as follows:

* **Command line** option

   |Parameter|Description|Declaration|
   |----|----|----|
   |create-if-not-exist|Create target table if it does not exist.|`--create-if-not-exist`|
   |dbpassword|Database password that is used to do ingestion. This is a mandatory parameter to run an ingestion job unless the default user is used.|`--dbpassword <DBPASSWORD>`|
   |dbuser|Database username that is used to do ingestion. This is a mandatory parameter to run an ingestion job unless the default user is used.|`--dbuser <DBUSER>`|
   |ingest-config|Configuration file for data migration|`--ingest-config <INGEST_CONFIGFILE>`|
   |ingestion-engine-endpoint|Endpoint of ingestion engine. hostname=`<hostname>`, port=`<port>`. This is a mandatory parameter to run an ingestion job.|`--ingestion-engine-endpoint <INGESTION_ENGINE_ENDPOINT>`|
   |log-directory|This option is used to specify the location of log files. See [Log directory]({{site.data.keyword.ref-cli_commands-link}}#log_direc).|`--ingest-config <ingest_config_file> --log-directory <directory_path>`|
   |schema|Schema file that includes CSV specifications, and more. See [Schema file specifications]({{site.data.keyword.ref-cli_commands-link}}#schema_spec).|`--schema </path/to/schemaconfig/file>`|
   |source-data-files|Data files or folders for data migration. File name ending with `/` is considered a folder. Single or multiple files can be used. This is a mandatory parameter to run an ingestion job. File names are case sensitive. Example: `<file1_path>,<file2_path>,<folder1_path>`|`--source-data-files <SOURCE_DATA_FILE>`|
   |staging-location|Location where CSV files and in some circumstances Parquet files are staged, see [Staging location]({{site.data.keyword.ref-cli_commands-link}}#stag_loc). This is a mandatory parameter to run an ingestion job.|`--staging-location <STAGING_LOCATION>`|
   |staging-hive-catalog|The Hive catalog name configured in the watsonx.data, if not using the default catalog for staging. Default catalog: hive_data.|`--staging-hive-catalog <catalog_name>`|
   |staging-hive-schema|The schema name associated with the staging Hive catalog for ingestion. Create and pass in a custom schema name by using this parameter. Default schema: `lhingest_staging_schema`. If schema is created as default, you do not have need to specify this parameter.|`--staging-hive-schema <schema_name>`|
   |system-config|This parameter is used to specify system related parameters. See [System config]({{site.data.keyword.ref-cli_commands-link}}#sys_config).|`--system-config <path/to/system/configfile>`|
   |target-table|Data migration target table. `<catalog>.<schema>.<table1>`. This is a mandatory parameter to run an ingestion job. Example: `<iceberg.demo.customer1>`|`--target-table <TARGET_TABLES>`|
   |trust-store-path|Path of the truststore to access the ingestion engine. This is used to establish SSL connections. This is a mandatory parameter to run an ingestion job.|`--trust-store-path <TRUST_STORE_PATH>`|
   |trust-store-password|Password of truststore to access the ingestion engine. This is used to establish SSL connections. This is a mandatory parameter to run an ingestion job.|`--trust-store-password <TRUST_STORE_PASSWORD>`|
   {: caption="Command line options and variables" caption-side="bottom"}

* **Configuration file** option

   The **Configuration file** contains a global ingest configuration section and multiple individual ingest configuration sections to run the ingestion job. The specifications of the individual ingestion sections override the specifications of the global ingestion section.

   * Global ingest config section

      |Parameter|Description|Declaration|
      |----|----|----|
      |create-if-not-exist|Create target table if not existed|`create-if-not-exist:<true/false>`|
      |ingestion-engine-endpoint|Specifies connection parameters of the ingestion engine. Endpoint of ingestion engine. hostname=`<hostname>`, port=`<port>`|`ingestion-engine:hostname=<hostname>, port=<port>`|
      |target-table|Data migration target table. Only one target table can be specified. `<catalog>.<schema>.<table1>`|`target-table:<table_name>`|
      {: caption="Global ingest config options and variables" caption-side="bottom"}

   * Individual ingest config section

      There can be multiple individual ingest sections in a configuration file option. Each individual ingest config sections will be ingested separately.
      {: note}

      |Parameter|Description|Declaration|
      |----|----|----|
      |create-if-not-exist|Create target table if it does not exist.|`create-if-not-exist`|
      |dbpassword|Database password that is used to do ingestion. This is a mandatory parameter to run an ingestion job unless the default user is used.|`dbpassword:<DBPASSWORD>`|
      |dbuser|Database username that is used to do ingestion. This is a mandatory parameter to run an ingestion job unless the default user is used.|`dbuser:<DBUSER>`|
      |ingestion-engine-endpoint|Endpoint of ingestion engine. hostname=`<hostname>`, port=`<port>`. This is a mandatory parameter to run an ingestion job.|`ingestion-engine-endpoint:<INGESTION_ENGINE_ENDPOINT>`|
      |schema|Schema file that includes CSV specifications, and more. See [Schema file specifications]({{site.data.keyword.ref-cli_commands-link}}#schema_spec)|`schema:/path/to/schemaconfig/file`|
      |source-files|Data files or folders for data migration. File name ending with `/` is considered a folder. This is a mandatory parameter to run an ingestion job.|`source-files:<SOURCE_DATA_FILE>`|
      |staging-location|Location where CSV files and in some circumstances Parquet files are staged, see [Staging location]({{site.data.keyword.ref-cli_commands-link}}#stag_loc). This is a mandatory parameter to run an ingestion job.|`staging-location:<STAGING_LOCATION>`|
      |staging-hive-catalog|The Hive catalog name configured in the watsonx.data, if not using the default catalog for staging. Default catalog: hive_data.|`--staging-hive-catalog <catalog_name>`|
      |staging-hive-schema|The schema name associated with the staging Hive catalog for ingestion. Create and pass in a custom schema name by using this parameter. Default schema: `lhingest_staging_schema`. If schema is created as default, you do not have need to specify this parameter.|`--staging-hive-schema <schema_name>`|
      |system-config|This parameter is used to specify system related parameters. See [System config]({{site.data.keyword.ref-cli_commands-link}}#sys_config).|`--system-config <path/to/system/configfile>`|
      |target-catalog-uri|Target catalog uri|`target-catalog-uri:<TARGET_CATALOG_URI>`|
      |target-table|Data migration target table. `<catalog>.<schema>.<table1>`. This is a mandatory parameter to run an ingestion job. Example: `<iceberg.demo.customer1>`|`target-table:<TARGET_TABLES>`|
      |target-table-storage|Target table file storage location|`target-table-storage:<TARGET_TABLE_STORAGE>`|
      |trust-store-path|Path of truststore to access ingestion engine. This is used to establish SSL connections. This is a mandatory parameter to run an ingestion job.|`trust-store-path:<TRUST_STORE_PATH>`|
      |trust-store-password|Password of truststore to access the ingestion engine. This is used to establish SSL connections. This is a mandatory parameter to run an ingestion job.|`trust-store-password:<TRUST_STORE_PASSWORD>`|
      {: caption="Individual ingest config options and variables" caption-side="bottom"}
