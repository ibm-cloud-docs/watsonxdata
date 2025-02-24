---

copyright:
  years: 2022, 2024
lastupdated: "2025-02-24"

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
* For the target table, an active Iceberg catalog connected to a running Presto engine is required. See [Adding a storage-catalog pair]({{site.data.keyword.ref-reg_bucket-link}}). The storage must have `Writer` access at minimum.
* To ingest data, you must have at minimum a `User` access to Presto engine and Spark engine.
* To ingest data, you must have at minimum a `User` access with data plicy for catalogs. See [Managing data policy rules](watsonxdata?topic=watsonxdata-data_policy).
* Add remote storage for source data files. See [Adding a storage-catalog pair]({{site.data.keyword.ref-reg_bucket-link}}).
* Add data sources for source data files. See [Adding a data source-catalog pair]({{site.data.keyword.ref-reg_database-link}}).
* Optionally, you can create a schema in the catalog for the target table. See [Creating schemas]({{site.data.keyword.ref-create_schema-link}}).
* Optionally, you can also create a target table in the schema. See [Creating tables]({{site.data.keyword.ref-create_table-link}}).
* To enable your Spark application and ingestion to work with the watsonx.data catalog and storage, you must have `MetastoreAdmin`, and `DataAccess` roles in the service access and `Administrator` role in the platform access, see [Assigning access to account management services](https://cloud.ibm.com/docs/account?topic=account-account-services&interface=ui) and [Managing roles and privileges]({{site.data.keyword.ref-role_priv-link}}).

## Ingesting data from local system
{: #spk_ingest_datalocal}

1. Log in to {{site.data.keyword.lakehouse_full}} console.
2. From the navigation menu, select **Data manager** and click **Ingest data**.
4. Select one of the following storage options to proceed to the next page:

   a. **Local System**: To select files from your local system.

   b. **Storages**: To select remote files from your connected S3 compatible storage.

   c. **Data sources**: To select files from your connected data sources.

5. If you selected **Local system**, complete the following steps:

   i. Drag a file to the box or click to upload. Selected files are listed in the **Selected file(s)** section.

       You can add multiple files of the same file type. The available file type options are CSV, Parquet, JSON, ORC, and AVRO. The maximum cumulative file size must be within 500 MB.
       {: note}

   ii. Select a transient storage bucket from the drop down to temporarily store uploaded files.

       The files are automatically deleted from this storage upon ingestion completion or failure. This is available only when ingesting data from a Local system.
       {: note}

   iii. Click **Next**.

   iv. In the **Ingest data: Local** page, you can see the details of the source files and upload more files if required.

       You can remove individual files and can also remove all the files by using the **Unselect all** option.
       {: note}

   v. Click the preview icon against the specific file that you want to preview. This action opens a new File preview window displaying the tables of the selected file.

   vi. Click the **Edit** button to edit the column headers.

   vii. Modify the column headers and column data types as required to make any transformation. Incorrect data type selection can result in ingestion error.

   viii. For CSV files, you can select the **Advanced attributes** to customize the file interpretation for the following:

      **Header in first row:** Select this option if the CSV file has a header row containing column names.

      **Column Delimiter:** Specify the character that is used to separate columns in the CSV file.

      **File Encoding:** Choose the character encoding used in the CSV file.

      **Row Delimiter:** Specify the character that is used to separate rows in the CSV file.

      **Escape Character:** Define the character used to escape special characters within the CSV file.

   ix. You can use **Cancel edit** or **Reset** to revert the column headers to their original state, if you need to undo your changes.

   x. Click **Save** to save the changes.

   xi. In the **Target table** section, select the target catalog from the **Select catalog** list. The selected catalog must be active to perform an ingestion job.

   xii. Choose one of the schema options:

      1.  Existing schema: To ingest source data into an existing schema. Search or select a target schema that is listed in the **Select schema** drop-down.

      2. New schema: Enter a new schema name in the **Create a new schema** field by explicitly clicking **Create** option to create a new schema from the source data.

   xiii. Select the corresponding target table options based on the preceding selection.

      1. Existing table: To ingest source data into an existing table. Search or select a target table that is listed in the **Select table** drop-down.

      2. New table: Enter a new target table name in the **Create a new table** field by explicitly clicking **Create** option to create a new table from the source data.

   xiv. If required, modify the auto-generated ingestion Job ID in the **Job Details**.

   xv. Select the IBM Analytics Engine (Spark) from the **Select engine** list. The registered Spark engines are listed here.

      Any files less than 2 MB file size shall automatically select Lite ingestion and all files more than 2 MB file size shall automatically select one of the listed Spark engines from the Select engine drop-down list to run the ingestion job.
      {: note}

      Lite ingestion is available only when ingesting data from a Local system.
      {: note}

   xvi. Select a pre-defined **Job size** from the options listed if the selected engine is a Spark engine. The job size is set to the preferred option based on the file size automatically. The user can also select one of the following options.

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

   xvii. Click **Preview** to view the final output table to be displayed in **Data manager**.

      If the selected target table is an existing table, the data is appended or overwritten with the new ingested data. Default action being append
      {: note}

   xviii. Click **Edit** to modify the column headers and column data types as required to make any transformation for the target table. You can also revert the changes if not required.

   xix. Click **Ingest**. The submitted ingestion job can be found in the **Ingestion history** tab of the **Data manager** page.

      A notification message **Open job details** is triggered to navigate to the Ingestion job details.
      {: note}

      You can cancel an ingestion job by clicking the **cancel** icon against the ingestion job from the **Ingestion history** tab or by clicking the **Cancel job** in the ingestion job details page.
      {: note}

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

   v. Click the **Edit** button to edit the column headers.

   vi. Modify the column headers and data types as required to make any transformation.

   vii. You can use **Cancel edit** or **Reset** to revert the column headers to their original state, if you need to undo your changes.

   viii For CSV files, you can select the Advanced attributes to customize the file interpretation for the following:

      **Header in first row:** Select this option if the CSV file has a header row containing column names.

      **Column Delimiter:** Specify the character that is used to separate columns in the CSV file.

      **File Encoding:** Choose the character encoding used in the CSV file.

      **Row Delimiter:** Specify the character that is used to separate rows in the CSV file.

      **Escape Character:** Define the character used to escape special characters within the CSV file.

   ix. Click **Save** to save the changes.

   x. In the **Target table** window, select the target catalog from the **Select catalog** list. The selected catalog must be active to perform an ingestion job.

   xi. Choose one of the schema options:

      1.  Existing schema: To ingest source data into an existing schema. Search or select a target schema that is listed in the **Select schema** drop-down.

      2. New schema: Enter a new schema name in the **Create a new schema** field by explicitly clicking **Create** option to create a new schema from the source data.

   xii. Select the corresponding Target table options based on the selection of schema.

      1. Existing table: To ingest source data into an existing table. Search or select a target table that is listed in the **Select table** drop-down.

      2. New table: Enter a new target table name in the **Create a new table** field by explicitly clicking **Create** option to create a new table from the source data.

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

   xvi.Click **Preview** to view the final output table to be displayed in **Data manager**.

      If the selected target table is an existing table, the data is appended or overwritten with the new ingested data. Default action being append
      {: note}

   xvii. Click **Edit** to modify the column headers and column data types as required to make any transformation for the target table. You can also revert the changes if not required.

   xviii. Click **Ingest**. The submitted ingestion job can be found in the **Ingestion history** tab of the **Data manager** page.

      A notification message **Open job details** is triggered to navigate to the Ingestion job details.
      {: note}

      You can cancel an ingestion job by clicking the **cancel** icon against the ingestion job from the **Ingestion history** tab or by clicking the **Cancel job** in the ingestion job details page.
      {: note}

## Ingesting data from databases
{: #spk_ingest_dataremote}

1. If you selected **Databases**, complete the following steps from the **Ingest data: Databases** page:

   i. Select a database from the **Select database** drop-down.

    You can also add a new database by clicking the **Add +** icon. For more information, see [Add Database]({{site.data.keyword.ref-reg_database-link}}). You can create a permanent database connection accessible to all users based on permissions in the infrastructure manager page by selecting **Create permanent connection**. You can also create a temporary database connection accessible to you for the time period during the ingestion by selecting **Create temporary connection**. This temporary database shall not be available in the infrastructure manager page or cannot be accessed by other users.
    {: note}

   ii. Select a schema from the **Schemas** window.

   iii. Select a table that you want to ingest from the **Browse Table** section.

   iv. In the **Target table** window, select the target catalog from the **Select catalog** list. The selected catalog must be active to perform an ingestion job.

   v. Choose one of the schema options:

      1.  Existing schema: To ingest source data into an existing schema. Search or select a target schema that is listed in the **Select schema** drop-down.

      2. New schema: Enter a new schema name in the **Create a new schema** field by explicitly clicking **Create** option to create a new schema from the source data.

   vi. Select the corresponding Target table options based on the selection (mentioned earlier).

      1. Existing table: To ingest source data into an existing table. Search or select a target table that is listed in the **Select table** drop-down.

      2. New table: Enter a new target table name in the **Create a new table** field by explicitly clicking **Create** option to create a new table from the source data.

   vii. If required, modify the auto-generated ingestion Job ID in the **Job Details**.

   viii. Select the IBM Analytics Engine (Spark) from the **Select engine** list. The registered Spark engines are listed here.

   ix. Select a pre-defined **Job size** from the options listed. The job size is set to the preferred option based on the file size automatically. The user can also select one of the following options.

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

   x.Click **Preview** to view the final output table to be displayed in **Data manager**.

      If the selected target table is an existing table, the data is appended or overwritten with the new ingested data. Default action being append
      {: note}

   xi. Click **Edit** to modify the column headers and column data types as required to make any transformation for the target table. You can also revert the changes if not required.

   xii. Click **Ingest**. The submitted ingestion job can be found in the **Ingestion history** tab of the **Data manager** page.

      A notification message **Open job details** is triggered to navigate to the Ingestion job details.
      {: note}

      You can cancel an ingestion job by clicking the **cancel** icon against the ingestion job from the **Ingestion history** tab or by clicking the **Cancel job** in the ingestion job details page.
      {: note}

   xiii. Click the required **Job log** ID of an ingestion job in the **Ingestion history** tab to get the details and logs.

   xiv. Click the **Target** link of an ingestion job in the **Ingestion history** tab to navigate to the ingested table in **Data manager** page.

## Related API
{: #ingestion_api}

For information on related API, see
* [Get ingestion jobs](https://cloud.ibm.com/apidocs/watsonxdata#list-ingestion-jobs)
* [Create an ingestion job](https://cloud.ibm.com/apidocs/watsonxdata#create-ingestion-jobs)
* [Create an ingestion job for user local files](https://cloud.ibm.com/apidocs/watsonxdata#create-ingestion-jobs-local-files)
* [Get ingestion job](https://cloud.ibm.com/apidocs/watsonxdata#get-ingestion-job)
* [Delete an ingestion job](https://cloud.ibm.com/apidocs/watsonxdata#delete-ingestion-jobs)
* [Generate a preview of source file(s)](https://cloud.ibm.com/apidocs/watsonxdata#create-preview-ingestion-file)
