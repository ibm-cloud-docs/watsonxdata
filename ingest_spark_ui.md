---

copyright:
  years: 2022, 2024
lastupdated: "2024-09-19"

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

* Add and register {{site.data.keyword.iae_full_notm}} (Spark). See [Provisioning a Spark engine](watsonxdata?topic=watsonxdata-spl_engine).
* Add storage for the source data files and target catalog. See [Adding a storage-catalog pair](watsonxdata?topic=watsonxdata-reg_bucket).
* Optionally, you can create a schema in the catalog for the target table. See [Creating schemas](watsonxdata?topic=watsonxdata-create_schema).
* Optionally, you can also create a target table in the schema. See [Creating tables](watsonxdata?topic=watsonxdata-create_table).
* To enable your Spark application and ingestion to work with the {{site.data.keyword.lakehouse_short}} catalog and storage, you must have `MetastoreAdmin`, and `DataAccess` roles in the Service access and `Administrator` role in the Platform access, see [Assigning access to account management services](https://cloud.ibm.com/docs/account?topic=account-account-services&interface=ui).

## Ingesting data
{: #spk_ingest_data}

1. Log in to {{site.data.keyword.lakehouse_full}} console.
2. From the navigation menu, select **Data manager**.
3. Click **Ingest data**. The **Ingest data** window opens.
4. Select one of the following storage options to proceed to the next page:

   a. **Local System**: To select your files from your local system.

   b. **Storages**: To select remote file(s) from your connected S3 compatible storages.

5. If you selected **Local system**, complete the following steps:

   i. Drag a file to the box or click to upload. Selected files are listed in the **Selected file(s)** section. Click **Next**.

    To preview a file, you can click on the preview icon against a file in the **Selected file(s)** section. You can add multiple files of same file type. The available file type options are CSV, Parquet, and JSON. The maximum file size must be 500 MB.
    {: note}

   ii. In the **Ingest data: Local** page, you can see the details of the source files and upload more files if required.

    You can remove individual files and also remove all files by using **Deselect all** option.
    {: note}

   iii. In the **Target table** section, select the target catalog from the **Select catalog** list. The selected catalog must be active to perform an ingestion job.

   iii. Choose one of the schema options:

      1.  Existing schema: To ingest source data into an existing schema. Search or select a target schema listed in the **Select schema or enter new schema name (New)** dropdown.

      2. New schema: Enter a new schema name in the **Select schema or enter new schema name** field and explicitly click **Create: `<new schema name>`** to create a new schema from the source data.

   iv. Select the corresponding Target table options based on the selection (above).

      1. Existing table: To ingest source data into an existing table. Search or select a target table listed in the **Select table or enter new table name** dropdown.

      2. New table: Enter a new target table name in the **Select table or enter new table name** and explicitly click **Create: `<new table name>`** to create a new table from the source data.

   v. If required, modify the auto-generated ingestion Job ID in the **Job Details**.

   vi. Select the IBM Analytics Engine (Spark) from the **Select engine** list. The registered Spark engines are listed here.

   vii. Click **Done**. The submitted ingestion job can be found in the **Ingestion history** tab of the **Data manager** page.

6. If you selected **Storages**, complete the following steps:

   i. Select a storage bucket from the **Select storage** drop-down.

    You can also add a new storage bucket by clicking the Add + icon. For more information, see [Add Storage](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-reg_bucket). The new storage can be permanent or temporary, you can make appropriate selection based on your requirement.
    {: note}

   ii. Select the required file type based on the source data. The available options are CSV, Parquet, and JSON.

   iii. Select the files to be ingested from the **All files** tab. Selected files are listed in the **Files selected** tab. You can see the details of the selected files in the **File details** section.

    To preview a file, you can click on the preview icon against a file in the **Files selected** tab. You can add multiple files of same file type. The maximum file size must be 500 MB.
    {: note}

    You can remove individual files and also remove all files by using **Deselect all** option.
    {: note}

   iv. In the **Target table** pane, select the target catalog from the **Select catalog** list. The selected catalog must be active to perform an ingestion job.

   v. Choose one of the schema options:

      1.  Existing schema: To ingest source data into an existing schema. Search or select a target schema listed in the **Select schema or enter new schema name (New)** dropdown.

      2. New schema: Enter a new schema name in the **Select schema or enter new schema name (New)** field and explicitly click **Create `<new schema name>`** to create a new schema from the source data.

   vi. Select the corresponding Target table options based on the selection (above).

      1. Existing table:To ingest source data into an existing table. Search or select a target table listed in the **Select table or enter new table name** dropdown.

      2. New table: Enter a new target table name in the **Select table or enter new table name** and explicitly click **Create `<new table name>`** to create a new table from the source data.

   vii. If required, modify the auto-generated ingestion Job ID in the **Job Details**.

   viii. Select the IBM Analytics Engine (Spark) from the **Select engine** list. The registered Spark engines are listed here.

   xi. Click **Done**. The submitted ingestion job can be found in the **Ingestion history** tab of the **Data manager** page.
