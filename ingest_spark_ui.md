---

copyright:
  years: 2022, 2024
lastupdated: "2024-10-30"

keywords: watsonx.data, data ingestion, source file

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

# Ingesting data by using Spark through the web console
{: #ingest_spark_ui}

You can ingest data into {{site.data.keyword.lakehouse_full}} through the web console. Ingestion through web console is supported only by using {{site.data.keyword.iae_full_notm}} (Spark).
{: shortdesc}

## Before you begin
{: #spk_ing}

* Add and register IBM Analytics Engine (Spark). See [Provisioning a Spark engine]({{site.data.keyword.ref-spl_engine-link}}).
* For the target table, an active Iceberg catalog connected to a running Presto engine is required. See [Adding a storage-catalog pair]({{site.data.keyword.ref-reg_bucket-link}}).
* Add remote storage for source data files. See [Adding a storage-catalog pair]({{site.data.keyword.ref-reg_bucket-link}}).
* Add data sources for source data files. See [Adding a data source-catalog pair]({{site.data.keyword.ref-reg_database-link}}).
* Optionally, you can create a schema in the catalog for the target table. See [Creating schemas]({{site.data.keyword.ref-create_schema-link}}).
* Optionally, you can also create a target table in the schema. See [Creating tables]({{site.data.keyword.ref-create_table-link}}).
* To enable your Spark application and ingestion to work with the watsonx.data catalog and storage, you must have `MetastoreAdmin`, and `DataAccess` roles in the service access and `Administrator` role in the platform access, see [Assigning access to account management services](https://cloud.ibm.com/docs/account?topic=account-account-services&interface=ui).

## Ingesting data from local system
{: #spk_ingest_datalocal}

1. Log in to {{site.data.keyword.lakehouse_full}} console.
2. From the navigation menu, select **Data manager** and click **Ingest data**.
4. Select one of the following storage options to proceed to the next page:

   a. **Local System**: To select files from your local system.

   b. **Storages**: To select remote files from your connected S3 compatible storage.

   c. **Data sources**: To select files from your connected data sources.

5. If you selected **Local system**, complete the following steps:

   i. Drag a file to the box or click to upload. Selected files are listed in the **Selected file(s)** section. Click **Next**.

    You can add multiple files of the same file type. The available file type options are CSV, Parquet, JSON, ORC, and AVRO. The maximum cumulative file size must be within 500 MB.
    {: note}

   ii. In the **Ingest data: Local** page, you can see the details of the source files and upload more files if required.

    You can remove individual files and can also remove all the files by using the **Unselect all** option.
    {: note}

   iii. Click the preview icon against the specific file that you want to preview. This action opens a new File preview window displaying the tables of the selected file.

   iv. Click the Edit button to edit the column headers.

   v. Modify the column headers as required to make any transformation.

   vi. You can use Cancel edit or Reset to revert the column headers to their original state, if you need to undo your changes.

   vii. For CSV files, you can select the **Advanced attributes** to customize the file interpretation for the following:

      **Header in first row:** Select this option if the CSV file has a header row containing column names.

      **Column Delimiter:** Specify the character that is used to separate columns in the CSV file.

      **File Encoding:** Choose the character encoding used in the CSV file.

      **Row Delimiter:** Specify the character that is used to separate rows in the CSV file.

      **Escape Character:** Define the character used to escape special characters within the CSV file.

   viii. Click **Save** to save the changes.

   viii. In the **Target table** section, select the target catalog from the **Select catalog** list. The selected catalog must be active to perform an ingestion job.

   ix. Choose one of the schema options:

      1.  Existing schema: To ingest source data into an existing schema. Search or select a target schema that is listed in the **Select schema or enter new schema name** drop-down.

      2. New schema: Enter a new schema name in the **Select schema or enter new schema name** field and explicitly click **+ Create new: `<new schema name>`** to create a new schema from the source data.

   x. Select the corresponding target table options based on the preceding selection.

      1. Existing table: To ingest source data into an existing table. Search or select a target table that is listed in the **Select table or enter new table name** drop-down. You can select **Append** or **Replace** to ingest data to the existing table. The default action being append.

      2. New table: Enter a new target table name in the **Select table or enter new table name** and explicitly click **+ Create new: `<new table name>`** to create a new table from the source data.

   xi. If required, modify the auto-generated ingestion Job ID in the **Job Details**.

   xii. Select the IBM Analytics Engine (Spark) from the **Select engine** list. The registered Spark engines are listed here.

   xiii. Select a pre-defined **Job size** from the options listed. The job size is set to the preferred option based on the file size automatically. The user can also select one of the following options.

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

   xiv. Click **Done**. The submitted ingestion job can be found in the **Ingestion history** tab of the **Data manager** page.

   xv. Click the cancel icon to cancel the ingestion job.

## Ingesting data from remote storage
{: #spk_ingest_dataremote}

1. If you selected **Storages**, complete the following steps from the **Ingest data: Storages** page:

   i. Select a storage bucket from the **Select storage** drop-down.

    You can also add a new storage bucket by clicking the **Add +** icon. For more information, see [Add Storage]({{site.data.keyword.ref-reg_bucket-link}}). You can create a permanent storage connection accessible to all users based on permissions. In the infrastructure manager page by selecting **Create permanent connection**. You can also create a temporary storage connection accessible to you for the time period during the ingestion by selecting **Create temporary connection**. This temporary storage shall not be available in the infrastructure manager page or cannot be accessed by other users.
    {: note}

   ii. Select the required file type based on the source data. The available options are CSV, Parquet, JSON, ORC, and AVRO.

   iii. Select the files to be ingested from the **All files** tab. Selected files are listed in the **Files selected** tab. You can see the details of the selected files in the **File details** section.

    You can add multiple files of the same file type. The maximum file size must be 500 MB.
    {: note}

    You can remove individual files and also remove all files by using **Unselect all** option.
    {: note}

   iv. Click the preview icon against the specific file that you want to preview. This action opens a new File preview window displaying the tables of the selected file.

   v. Click the Edit button to edit the column headers.

   vi. Modify the column headers as required to make any transformation.

   vii. You can use Cancel edit or Reset to revert the column headers to their original state, if you need to undo your changes.

   viii For CSV files, you can select the Advanced attributes to customize the file interpretation for the following:

      **Header in first row:** Select this option if the CSV file has a header row containing column names.

      **Column Delimiter:** Specify the character that is used to separate columns in the CSV file.

      **File Encoding:** Choose the character encoding used in the CSV file.

      **Row Delimiter:** Specify the character that is used to separate rows in the CSV file.

      **Escape Character:** Define the character used to escape special characters within the CSV file.

   ix. Click **Save** to save the changes.

   x. In the **Target table** window, select the target catalog from the **Select catalog** list. The selected catalog must be active to perform an ingestion job.

   xi. Choose one of the schema options:

      1.  Existing schema: To ingest source data into an existing schema. Search or select a target schema that is listed in the **Select schema or enter new schema name** dropdown.

      2. New schema: Enter a new schema name in the **Select schema or enter new schema name** field and explicitly click **+ Create new: `<new schema name>`** to create a new schema from the source data.

   xii. Select the corresponding Target table options based on the selection (mentioned earlier).

      1. Existing table: To ingest source data into an existing table. Search or select a target table that is listed in the **Select table or enter new table name** drop-down. You can select **Append** or **Replace** to ingest data to the existing table. The default action being append.

      2. New table: Enter a new target table name in the **Select table or enter new table name** and explicitly click **+ Create new: `<new table name>`** to create a new table from the source data.

   xiii. If required, modify the auto-generated ingestion Job ID in the **Job Details**.

   xiv. Select the IBM Analytics Engine (Spark) from the **Select engine** list. The registered Spark engines are listed here.

   xv. Select a pre-defined **Job size** from the options listed. The job size is set to the preferred option based on the file size automatically. The user can also select one of the following options.

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

   xvi. Click **Done**. The submitted ingestion job can be found in the **Ingestion history** tab of the **Data manager** page.

   xvii. Click the cancel icon to cancel the ingestion job.

## Ingesting data from databases
{: #spk_ingest_dataremote}

1. If you selected **Databases**, complete the following steps from the **Ingest data: Databases** page:

   i. Select a database from the **Select database** drop-down.

    You can also add a new database by clicking the **Add +** icon. For more information, see [Add Database]({{site.data.keyword.ref-reg_database-link}}). You can create a permanent database connection accessible to all users based on permissions in the infrastructure manager page by selecting **Create permanent connection**. You can also create a temporary database connection accessible to you for the time period during the ingestion by selecting **Create temporary connection**. This temporary database shall not be available in the infrastructure manager page or cannot be accessed by other users.
    {: note}

   ii. Select a schema from the **Schemas** window.

   iii. Select a table that you want to ingest from the **Browse Table** section.

   x. In the **Target table** window, select the target catalog from the **Select catalog** list. The selected catalog must be active to perform an ingestion job.

   xi. Choose one of the schema options:

      1.  Existing schema: To ingest source data into an existing schema. Search or select a target schema that is listed in the **Select schema or enter new schema name** dropdown.

      2. New schema: Enter a new schema name in the **Select schema or enter new schema name** field and explicitly click **+ Create new: `<new schema name>`** to create a new schema from the source data.

   xii. Select the corresponding Target table options based on the selection (mentioned earlier).

      1. Existing table: To ingest source data into an existing table. Search or select a target table that is listed in the **Select table or enter new table name** drop-down. You can select **Append** or **Replace** to ingest data to the existing table. The default action being append.

      2. New table: Enter a new target table name in the **Select table or enter new table name** and explicitly click **+ Create new: `<new table name>`** to create a new table from the source data.

   xiii. If required, modify the auto-generated ingestion Job ID in the **Job Details**.

   xiv. Select the IBM Analytics Engine (Spark) from the **Select engine** list. The registered Spark engines are listed here.

   xv. Select a pre-defined **Job size** from the options listed. The job size is set to the preferred option based on the file size automatically. The user can also select one of the following options.

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

   xvi. Click **Done**. The submitted ingestion job can be found in the **Ingestion history** tab of the **Data manager** page.

   xvii. Click the cancel icon to cancel the ingestion job.
