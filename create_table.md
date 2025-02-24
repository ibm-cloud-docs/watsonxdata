---

copyright:
  years: 2022, 2024
lastupdated: "2025-02-24"

keywords: watsonxdata, data manager, create table

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

# Creating table
{: #create_table}

You can generate, configure, and run DDL from the **Data manager** page by using the web console.
{: shortdesc}

## Before you begin
{: #create_tablebyb}

* A schema must be created. See [Creating svchema](watsonxdata?topic=watsonxdata-create_schema).
* Add and register IBM Analytics Engine (Spark). See [Provisioning a Spark engine]({{site.data.keyword.ref-spl_engine-link}}).
* For the target table, an active Iceberg catalog connected to a running Presto engine is required. See [Adding a storage-catalog pair]({{site.data.keyword.ref-reg_bucket-link}}). The storage must have `Writer` access at minimum.
* To ingest data, you must have at minimum a `User` access to Presto engine and Spark engine.

## Procedure
{: #create_tableprc}

1. Log in to {{site.data.keyword.lakehouse_full}} console.
1. From the navigation menu, select **Data manager**, click **Browse data**.
1. Select the engine from the **Engine** menu. Catalogs that are associated with the selected engine are listed.
1. There are two ways to import a file into a table. Select the required option.

   Option 1: To import file to any available schema under a catalog, do the following steps:
   1. Click Create drop-down.
   1. Click **Create table from file**. The **Create table from file** page opens.
   1. Go to step 5.

   Option 2: To import file to a particular schema under the catalog, do the following steps:
   1. Select a schema under a catalog where you want to import a file to create table.
   1. Click the overflow menu of the selected schema and select **Create table from file**. The **Create table from file** page opens.
   1. Go to step 5.

1. Drag a file to the box or click to upload. Selected files are listed in the **Selected file(s)** section.

   You can add multiple files of the same file type. The available file type options are CSV, Parquet, JSON, ORC, and AVRO. The maximum cumulative file size must be within 500 MB.
   {: note}

1. Select a transient storage bucket from the drop down to temporarily store uploaded files.

   The files are automatically deleted from this storage upon ingestion completion or failure. This is available only when ingesting data from a Local system.
   {: note}

1. Click **Next**.

1. In the **Ingest data: Local** page, you can see the details of the source files and upload more files if required.

   You can remove individual files and can also remove all the files by using the **Unselect all** option.
   {: note}

1. Click the preview icon against the specific file that you want to preview. This action opens a new File preview window displaying the tables of the selected file.

1. Click the **Edit** button to edit the column headers.

1. Modify the column headers and column data types as required to make any transformation. Incorrect data type selection can result in ingestion error.

1. For CSV files, you can select the **Advanced attributes** to customize the file interpretation for the following:

   **Header in first row:** Select this option if the CSV file has a header row containing column names.

   **Column Delimiter:** Specify the character that is used to separate columns in the CSV file.

   **File Encoding:** Choose the character encoding used in the CSV file.

   **Row Delimiter:** Specify the character that is used to separate rows in the CSV file.

   **Escape Character:** Define the character used to escape special characters within the CSV file.

1. You can use **Cancel edit** or **Reset** to revert the column headers to their original state, if you need to undo your changes.

1. Click **Save** to save the changes.

1. In the **Target table** section, select the target catalog from the **Select catalog** list. The selected catalog must be active to perform an ingestion job.

1. Choose one of the schema options:

   1.  Existing schema: To ingest source data into an existing schema. Search or select a target schema that is listed in the **Select schema or enter new schema name** drop-down.

   2. New schema: Enter a new schema name in the **Select schema or enter new schema name** field and explicitly click **+ Create new: `<new schema name>`** to create a new schema from the source data.

1. Select the corresponding target table options based on the preceding selection.

   1. Existing table: To ingest source data into an existing table. Search or select a target table that is listed in the **Select table or enter new table name** drop-down.

   2. New table: Enter a new target table name in the **Select table or enter new table name** and explicitly click **+ Create new: `<new table name>`** to create a new table from the source data.

1. If required, modify the auto-generated ingestion Job ID in the **Job Details**.

1. Select the IBM Analytics Engine (Spark) from the **Select engine** list. The registered Spark engines are listed here.

   Any files less than 2 MB file size shall automatically select Lite ingestion and all files more than 2 MB file size shall automatically select one of the listed Spark engines from the Select engine drop-down list to run the ingestion job.
   {: note}

   Lite ingestion is available only when ingesting data from a Local system.
   {: note}

1. Select a pre-defined **Job size** from the options listed if the selected engine is a Spark engine. The job size is set to the preferred option based on the file size automatically. The user can also select one of the following options.

   **Local:**

   |Configuration|Value|
   |----|----|
   |Number of executors|1|
   |Executor cores|2 vCPU|
   |Executor memory|4 GB|
   {: caption="Local configuration."}

   **Small:**

   |Configuration|Value|
   |----|----|
   |Driver memory|2 GB|
   |Driver cores|1 vCPU|
   |Number of executors|1|
   |Executor cores|1 vCPU|
   |Executor memory|2 GB|
   {: caption="Small configuration."}

   **Medium:**

   |Configuration|Value|
   |----|----|
   |Driver memory|4 GB|
   |Driver cores|2 vCPU|
   |Number of executors|2|
   |Executor cores|2 vCPU|
   |Executor memory|4 GB|
   {: caption="Medium configuration."}

   **Large:**

   |Configuration|Value|
   |----|----|
   |Driver memory|8 GB|
   |Driver cores|4 vCPU|
   |Number of executors|4|
   |Executor cores|4 vCPU|
   |Executor memory|8 GB|
   {: caption="Large configuration."}

1. Click **Preview** to view the final output table to be displayed in **Data manager**.

   If the selected target table is an existing table, the data is appended or overwritten with the new ingested data. Default action being append
   {: note}

1. Click **Edit** to modify the column headers and column data types as required to make any transformation for the target table. You can also revert the changes if not required.

1. Click **Ingest**. The submitted ingestion job can be found in the **Ingestion history** tab of the **Data manager** page.

   A notification message **Open job details** is triggered to navigate to the Ingestion job details.
   {: note}

   You can cancel an ingestion job by clicking the **cancel** icon against the ingestion job from the **Ingestion history** tab or by clicking the **Cancel job** in the ingestion job details page.
   {: note}

## Related API
{: #table_api}

For information on related API, see
* [List all tables](https://cloud.ibm.com/apidocs/watsonxdata-software#list-tables)
* [Get table details](https://cloud.ibm.com/apidocs/watsonxdata-software#get-table)
* [Delete table](https://cloud.ibm.com/apidocs/watsonxdata-software#delete-table)
* [Rename table](https://cloud.ibm.com/apidocs/watsonxdata-software#update-table)
* [Get all tables](https://cloud.ibm.com/apidocs/watsonxdata#list-all-tables)
* [Get table details](https://cloud.ibm.com/apidocs/watsonxdata#get-table-details)
