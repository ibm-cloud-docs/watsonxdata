---

copyright:
  years: 2022, 2025
lastupdated: "2025-06-26"

keywords: lakehouse, cpdctl, watsonx.data, supporting commands, wx-data

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

# wx-data Commands and Usage
{: #cpdctl_commands_wxdata}

The `wx-data` command further has different commands within, using which you can perform various operations specific to {{site.data.keyword.lakehouse_full}}. This topic lists the commands with a brief description of the tasks that can be performed.

The `wx-data` command performs operations such as ingesting data, managing engines, storage, and data sources in {{site.data.keyword.lakehouse_short}}.

Syntax:
   ```bash
   ./cpdctl wx-data [command] [options]
   ```
   {: codeblock}


The wx-data command supports the following commands:

- `ingestion`
- `engine`
- `bucket`
- `database`
- `sparkjob`
- `tablemaint`
- `service`

## How to Use `wx-data` Command --help (-h)
{: #cpdctl_commands_wxdatahwto}

To list all the commands in the `wx-data` plugin:
   ```bash
   ./cpdctl wx-data --help
   ```
   {: codeblock}

To get details of all options and its descriptions for a specific command in `wx-data` plugin:
   ```bash
   ./cpdctl wx-data [command] --help
   ```
   {: codeblock}

For example:

   ```bash
   ./cpdctl wx-data ingestion -h
   NAME:
      ingestion - Commands for Ingestion resource.

   USAGE:
      cpdctl wx-data ingestion [action]

   COMMANDS:
      list     List ingestion jobs.
      create   Create an ingestion job.
      get      Get ingestion job details.

   GLOBAL OPTIONS:
         --cpd-config string   Configuration file path
         --cpdconfig string    [Deprecated] Use --cpd-config instead
     -h, --help                Show help
         --profile string      Name of the configuration profile to use
     -q, --quiet               Suppresses verbose messages.
         --raw-output          If set to true, single values in JSON output mode are not surrounded by quotes

   Use "cpdctl wx-data ingestion service-command --help" for more information about a command.
   ```
   {: screen}

To get the details of all available options and arguments in the wx-data commands to execute an operation:
   ```bash
   ./cpdctl wx-data [command] [options] --help
   ```
   {: codeblock}

To use the wx-data plugin to execute an operation:
   ```bash
   ./cpdctl wx-data [command] [options]
   ```
   {: codeblock}


## ingestion
{: #cpdctl_commands_wxdataingst}

The `ingestion` command is used for executing different ingestion operations in {{site.data.keyword.lakehouse_short}}.

Syntax:
   ```bash
   ./cpdctl wx-data ingestion [options]
   ```
   {: codeblock}

The `ingestion` command further supports the following commands:

| Command | Description |
|---------|-------------|
| `./cpdctl wx-data ingestion list` | Lists the ingestion jobs executed in {{site.data.keyword.lakehouse_short}} instance. |
| `./cpdctl wx-data ingestion create` | Create an ingestion job in {{site.data.keyword.lakehouse_short}} instance. |
| `./cpdctl wx-data ingestion get` | Get the details of an ingestion job executed in {{site.data.keyword.lakehouse_short}} instance. |
 {: caption="Supported commands by ingestion" caption-side="bottom"}


## engine
{: #cpdctl_commands_wxdataeng}

The `engine` command is used for executing different engine-related operations in {{site.data.keyword.lakehouse_short}}.

Syntax:
   ```bash
   ./cpdctl wx-data engine [options]
   ```
   {: codeblock}

The `engine` command further supports the following commands:

| Command | Description |
|---------|-------------|
| `./cpdctl wx-data engine list` | Lists all the engines available in {{site.data.keyword.lakehouse_short}} instance. |
| `./cpdctl wx-data engine create` | Create or register an engine in {{site.data.keyword.lakehouse_short}} instance. |
| `./cpdctl wx-data engine delete` | Delete an engine from {{site.data.keyword.lakehouse_short}} instance. |
| `./cpdctl wx-data engine attach` | Associate catalogs to a Presto engine in {{site.data.keyword.lakehouse_short}} instance. |
| `./cpdctl wx-data engine detach` | Disassociate the catalogs associated with a Presto engine in {{site.data.keyword.lakehouse_short}} instance. |
 {: caption="Supported commands by engine" caption-side="bottom"}

## bucket
{: #cpdctl_commands_wxdatabuck}

The `bucket` command is used for executing different storage-related operations in {{site.data.keyword.lakehouse_short}}.

Syntax:
   ```bash
   ./cpdctl wx-data bucket [options]
   ```
   {: codeblock}

The `bucket` command further supports the following commands:

| Command | Description |
|---------|-------------|
| `./cpdctl wx-data bucket list` | Lists all the storages available in {{site.data.keyword.lakehouse_short}} instance. |
| `./cpdctl wx-data bucket create` | Register a storage in {{site.data.keyword.lakehouse_short}} instance. |
| `./cpdctl wx-data bucket get` | Get the details of a registered storage in {{site.data.keyword.lakehouse_short}} instance. |
| `./cpdctl wx-data bucket delete` | Delete a storage from {{site.data.keyword.lakehouse_short}} instance. |
| `./cpdctl wx-data bucket activate` | Activate a storage bucket in {{site.data.keyword.lakehouse_short}} on IBM Cloud instance only. |
| `./cpdctl wx-data bucket deactivate` | Deactivate a storage bucket in {{site.data.keyword.lakehouse_short}} on IBM Cloud instance only. |
 {: caption="Supported commands by bucket" caption-side="bottom"}

## database
{: #cpdctl_commands_wxdatadatabs}

The `database` command is used for executing different data source-related operations in {{site.data.keyword.lakehouse_short}}.

Syntax:
   ```bash
   ./cpdctl wx-data database [options]
   ```
   {: codeblock}

The `database` command further supports the following commands:

| Command | Description |
|---------|-------------|
| `./cpdctl wx-data database list` | Lists all the data sources available in {{site.data.keyword.lakehouse_short}} instance. |
| `./cpdctl wx-data database create` | Create or add a data source in {{site.data.keyword.lakehouse_short}} instance. |
| `./cpdctl wx-data database get` | Get the details of a registered data source in {{site.data.keyword.lakehouse_short}} instance. |
| `./cpdctl wx-data database delete` | Delete a data source from {{site.data.keyword.lakehouse_short}} instance. |
 {: caption="Supported commands by database" caption-side="bottom"}

## sparkjob
{: #cpdctl_commands_wxdatasprkjb}

The `sparkjob` command is used for executing different Spark-related operations in {{site.data.keyword.lakehouse_short}} version 2.1.2 and later.

Syntax:
   ```bash
   ./cpdctl wx-data sparkjob [options]
   ```
   {: codeblock}

The `sparkjob` command further supports the following commands:

| Command | Description |
|---------|-------------|
| `./cpdctl wx-data sparkjob list` | List all applications available in a Spark engine. |
| `./cpdctl wx-data sparkjob create` | Submit a Spark application. |
| `./cpdctl wx-data sparkjob get` | Get the status of a Spark application. |
 {: caption="Supported commands by sparkjob" caption-side="bottom"}

For more information about how to perform Spark table maintenance by using IBM cpdctl in {{site.data.keyword.lakehouse_short}} on IBM Software Hub, see [Spark table maintenance](https://www.ibm.com/docs/en/watsonx/watsonxdata/2.1.x?topic=engine-spark-table-maintenance-by-using-cpdctl) and for watsonx.data on IBM Cloud, see [Spark table maintenance](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-table-run_samp_file).

## tablemaint
{: #cpdctl_commands_tabmaint}

The tablemaint command is used for executing different Iceberg table maintenance operations in watsonx.data.

This is now applicable only for Amazon S3 storage.
{: important}

Syntax:
   ```bash
   ./cpdctl wx-data tablemaint [options]
   ```
   {: codeblock}


The tablemaint command supports the following commands:

| Options | Description |
|---------|-------------|
|`./cpdctl wx-data tablemaint rollback-to-snapshot`|Roll back, or restore the table to a specific snapshot ID.|
|`./cpdctl wx-data tablemaint rollback-to-timestamp`	|Roll back a table to the snapshot at a specific timestamp.|
|`./cpdctl wx-data tablemaint set-current-snapshot`	|Sets the current snapshot ID for a table.|
|`./cpdctl wx-data tablemaint cherrypick-snapshot`	|Cherry-picks changes from a snapshot into the current table state. Cherry-picking creates a new snapshot from an existing snapshot without altering or removing the original.|
|`./cpdctl wx-data tablemaint expire-snapshot` |Remove older snapshots and their files which are no longer needed.|
|`./cpdctl wx-data tablemaint remove-orphan` |Remove files that are not referenced in any metadata files of an Iceberg table and can thus be considered "orphaned".|
|`./cpdctl wx-data tablemaint rewrite-data`	|Rewrites the data files.|
|`./cpdctl wx-data tablemaint rewrite-manifests`	|Rewrite manifests for a table to optimize scan planning.|
|`./cpdctl wx-data tablemaint register-table`	|Creates a table.|
 {: caption="Supported commands by tablemaint" caption-side="bottom"}


The following flags are listed when you run each table maintenance command:

   * Force : If the value is set to TRUE, the SQL query that you are going to run will be printed.

   * Debug : If the value is set to TRUE, a copy of the Spark application file is stored to our computer.

## service
{: #cpdctl_commands_wxdatasvce}

The `service` command is used for executing different serviceability related operations in {{site.data.keyword.lakehouse_short}}.

Syntax:
   ```bash
   ./cpdctl wx-data service [options]
   ```
   {: codeblock}

The `service` command further supports the following commands:

| Command | Description |
|---------|-------------|
| `./cpdctl wx-data service list-tables` | Lists all table names of hive or iceberg connectors in {{site.data.keyword.lakehouse_short}} instance.|
| `./cpdctl wx-data service get-qhmm-config` | Get the qhmm enabled bucket name in {{site.data.keyword.lakehouse_short}} instance. |
| `./cpdctl wx-data service monitor` | To run stats and qhmm related queries in {{site.data.keyword.lakehouse_short}} instance. |
 {: caption="Supported commands by service" caption-side="bottom"}
