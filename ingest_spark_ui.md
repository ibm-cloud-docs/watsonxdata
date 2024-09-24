---

copyright:
  years: 2022, 2024
lastupdated: "2024-09-24"

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

* Add and register IBM Analytics Engine (Spark). See [Provisioning a Spark engine](watsonxdata?topic=watsonxdata-spl_engine).
* For target table, Iceberg catalog connected to Presto engine is required. See [Adding a storage-catalog pair](watsonxdata?topic=watsonxdata-reg_bucket).
* Add remote storage for source data files. See [Adding a storage-catalog pair](watsonxdata?topic=watsonxdata-reg_bucket).
* Add data sources for source data files. See [Adding a data source-catalog pair](watsonxdata?topic=watsonxdata-reg_database).
* Optionally, you can create a schema in the catalog for the target table. See [Creating schemas](watsonxdata?topic=watsonxdata-create_schema).
* Optionally, you can also create a target table in the schema. See [Creating tables](watsonxdata?topic=watsonxdata-create_table).
* To enable your Spark application and ingestion to work with the watsonx.data catalog and storage, you must have `MetastoreAdmin`, and `DataAccess` roles in the service access and `Administrator` role in the platform access, see [Assigning access to account management services](https://cloud.ibm.com/docs/account?topic=account-account-services&interface=ui).

## Ingesting data from local system
{: #spk_ingest_datalocal}

1. Log in to {{site.data.keyword.lakehouse_full}} console.
2. From the navigation menu, select **Data manager** and click **Ingest data**.
4. Select one of the following storage options to proceed to the next page:

   a. **Local System**: To select your files from your local system.

   b. **Storages**: To select remote files from your connected S3 compatible storage.

   c. **Data sources**: To select your files from your connected data sources.

5. If you selected **Local system**, complete the following steps:

   i. Drag a file to the box or click to upload. Selected files are listed in the **Selected file(s)** section. Click **Next**.

    You can add multiple files of same file type. The available file type options are CSV, Parquet, JSON, ORC, and AVRO. The maximum file size must be 500 MB.
    {: note}

   ii. In the **Ingest data: Local** page, you can see the details of the source files and upload more files if required.

    You can remove individual files and can also remove all the files by using the **Unselect all** option.
    {: note}

   iii. Click the preview icon against the specific file you want to preview. This action will open a new File preview window displaying the tables of the selected file.

   iv. Click the Edit button to edit the column headers.

   v. Modify the column headers as required to make any transformation.

   vi. You can use Cancel edit or Reset to revert the column headers to their original state, if you need to undo your changes.

   vii. For CSV files, you can select the **Advanced attributes** to customize the file interpretation for the following:

      **Header in first row:** Select this option if the CSV file has a header row containing column names.

      **Column Delimiter:** Specify the character used to separate columns in the CSV file.

      **File Encoding:** Choose the character encoding used in the CSV file.

      **Row Delimiter:** Specify the character used to separate rows in the CSV file.

      **Escape Character:** Define the character used to escape special characters within the CSV file.

   viii. Click **Save** to save the changes.

   viii. In the **Target table** section, select the target catalog from the **Select catalog** list. The selected catalog must be active to perform an ingestion job.

   ix. Choose one of the schema options:

      1.  Existing schema: To ingest source data into an existing schema. Search or select a target schema listed in the **Select schema or enter new schema name (New)** drop-down.

      2. New schema: Enter a new schema name in the **Select schema or enter new schema name** field and explicitly click **Create: `<new schema name>`** to create a new schema from the source data.

   x. Select the corresponding target table options based on the selection above.

      1. Existing table: To ingest source data into an existing table. Search or select a target table listed in the **Select table or enter new table name** drop-down.

      2. New table: Enter a new target table name in the **Select table or enter new table name** and explicitly click **Create: `<new table name>`** to create a new table from the source data.

   xi. If required, modify the auto-generated ingestion Job ID in the **Job Details**.

   xii. Select the IBM Analytics Engine (Spark) from the **Select engine** list. The registered Spark engines are listed here.

   xiii. Select a pre-defined **Job size** from the options listed:

      **Small:** Driver memory (GB): 2GB, Driver cores: 1 vCPU, Number of executors: 1, Executor cores: 1 vCPU, and Executor memory (GB): 2GB.

      **Medium:** Driver memory (GB): 4GB, Driver cores: 2 vCPU, Number of executors: 2, Executor cores: 2 vCPU, and Executor memory (GB): 4GB.

      **Large:** Driver memory (GB): 8GB, Driver cores: 4 vCPU, Number of executors: 4, Executor cores: 4 vCPU, and Executor memory (GB): 8GB.

   xiv. Click **Done**. The submitted ingestion job can be found in the **Ingestion history** tab of the **Data manager** page.

## Ingesting data from remote storage
{: #spk_ingest_dataremote}

1. If you selected **Storages**, complete the following steps from the **Ingest data: Storages** page:

   i. Select a storage bucket from the **Select storage** drop-down.

    You can also add a new storage bucket by clicking the **Add +** icon. For more information, see [Add Storage](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-reg_bucket). You can create a permanent storage connections accessible to all users based on permissions. in the infrastructure manager page by selecting **Keep permanent on infrastructure manager**. You can also create a temporary storage connections accessible to you for the time period during the ingestion by selecting **Temporary Database**. This temporary storage shall not be available in the infrastructure manager page nor can be accessed by other users.
    {: note}

   ii. Select the required file type based on the source data. The available options are CSV, Parquet, and JSON.

   iii. Select the files to be ingested from the **All files** tab. Selected files are listed in the **Files selected** tab. You can see the details of the selected files in the **File details** section.

    You can add multiple files of same file type. The maximum file size must be 500 MB.
    {: note}

    You can remove individual files and also remove all files by using **Deselect all** option.
    {: note}

   iv. Click the preview icon against the specific file you want to preview. This action will open a new File preview window displaying the tables of the selected file.

   v. Click the Edit button to edit the column headers.

   vi. Modify the column headers as required to make any transformation.

   vii. You can use Cancel edit or Reset to revert the column headers to their original state, if you need to undo your changes.

   viii For CSV files, you can select the Advanced attributes to customize the file interpretation for the following:

      **Header in first row:** Select this option if the CSV file has a header row containing column names.

      **Column Delimiter:** Specify the character used to separate columns in the CSV file.

      **File Encoding:** Choose the character encoding used in the CSV file.

      **Row Delimiter:** Specify the character used to separate rows in the CSV file.

      **Escape Character:** Define the character used to escape special characters within the CSV file.

   ix. Click **Save** to save the changes.

   x. In the **Target table** pane, select the target catalog from the **Select catalog** list. The selected catalog must be active to perform an ingestion job.

   xi. Choose one of the schema options:

      1.  Existing schema: To ingest source data into an existing schema. Search or select a target schema listed in the **Select schema or enter new schema name (New)** dropdown.

      2. New schema: Enter a new schema name in the **Select schema or enter new schema name (New)** field and explicitly click **Create `<new schema name>`** to create a new schema from the source data.

   xii. Select the corresponding Target table options based on the selection (above).

      1. Existing table:To ingest source data into an existing table. Search or select a target table listed in the **Select table or enter new table name** dropdown.

      2. New table: Enter a new target table name in the **Select table or enter new table name** and explicitly click **Create `<new table name>`** to create a new table from the source data.

   xiii. If required, modify the auto-generated ingestion Job ID in the **Job Details**.

   xiv. Select the IBM Analytics Engine (Spark) from the **Select engine** list. The registered Spark engines are listed here.

   xv. Select a pre-defined **Job size** from the options listed:

      **Small:** Driver memory (GB): 2GB, Driver cores: 1 vCPU, Number of executors: 1, Executor cores: 1 vCPU, and Executor memory (GB): 2GB.

      **Medium:** Driver memory (GB): 4GB, Driver cores: 2 vCPU, Number of executors: 2, Executor cores: 2 vCPU, and Executor memory (GB): 4GB.

      **Large:** Driver memory (GB): 8GB, Driver cores: 4 vCPU, Number of executors: 4, Executor cores: 4 vCPU, and Executor memory (GB): 8GB.

   xvi. Click **Done**. The submitted ingestion job can be found in the **Ingestion history** tab of the **Data manager** page.

## Ingesting data from databases
{: #spk_ingest_dataremote}

1. If you selected **Databases**, complete the following steps from the **Ingest data: Databases** page:

   i. Select a database from the **Select database** drop-down.

    You can also add a new database by clicking the **Add +** icon. For more information, see [Add Database](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-reg_database). You can create a permanent database connections accessible to all users based on permissions in the infrastructure manager page by selecting **Keep permanent on infrastructure manager**. You can also create a temporary database connections accessible to you for the time period during the ingestion by selecting **Temporary Database**. This temporary database shall not be available in the infrastructure manager page nor can be accessed by other users.
    {: note}

   ii. Select a schema from the **Schemas** window.

   iii. Select a table you want to ingest from the **Browse Table** section.

   x. In the **Target table** pane, select the target catalog from the **Select catalog** list. The selected catalog must be active to perform an ingestion job.

   xi. Choose one of the schema options:

      1.  Existing schema: To ingest source data into an existing schema. Search or select a target schema listed in the **Select schema or enter new schema name (New)** dropdown.

      2. New schema: Enter a new schema name in the **Select schema or enter new schema name (New)** field and explicitly click **Create `<new schema name>`** to create a new schema from the source data.

   xii. Select the corresponding Target table options based on the selection (above).

      1. Existing table:To ingest source data into an existing table. Search or select a target table listed in the **Select table or enter new table name** dropdown.

      2. New table: Enter a new target table name in the **Select table or enter new table name** and explicitly click **Create `<new table name>`** to create a new table from the source data.

   xiii. If required, modify the auto-generated ingestion Job ID in the **Job Details**.

   xiv. Select the IBM Analytics Engine (Spark) from the **Select engine** list. The registered Spark engines are listed here.

   xv. Select a pre-defined **Job size** from the options listed:

      **Small:** Driver memory (GB): 2GB, Driver cores: 1 vCPU, Number of executors: 1, Executor cores: 1 vCPU, and Executor memory (GB): 2GB.

      **Medium:** Driver memory (GB): 4GB, Driver cores: 2 vCPU, Number of executors: 2, Executor cores: 2 vCPU, and Executor memory (GB): 4GB.

      **Large:** Driver memory (GB): 8GB, Driver cores: 4 vCPU, Number of executors: 4, Executor cores: 4 vCPU, and Executor memory (GB): 8GB.

   xvi. Click **Done**. The submitted ingestion job can be found in the **Ingestion history** tab of the **Data manager** page.
