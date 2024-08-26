---

copyright:
  years: 2022, 2024
lastupdated: "2024-08-26"

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

* You must have the **Administrator** role and privileges in the catalog to do ingestion through the web console.
* Add and register {{site.data.keyword.iae_full_notm}} (Spark). See [Registering an engine]({{site.data.keyword.ref-reg_engine-link}}).
* Add storage for the source data files and target catalog. See [Adding a bucket-catalog pair]({{site.data.keyword.ref-reg_bucket-link}}).
* Optionally, you can create a schema in the catalog for the target table. See [Creating schemas]({{site.data.keyword.ref-create_schema-link}}).
* Optionally, you can also create a target table in the schema. See [Creating tables]({{site.data.keyword.ref-create_table-link}}).

## Ingesting data
{: #spk_ingest_data}

1. Log in to {{site.data.keyword.lakehouse_full}} console.
1. From the navigation menu, select **Data manager**.
1. Select the **Ingest data** tab and click **Create ingestion job**. The **Ingest data** window opens with an auto-generated job ID.
1. If required, modify the auto-generated ingestion job ID in the **Enter job ID** field.
1. Select the IBM Analytics Engine (Spark) from the **Select engine** list. The registered Spark engines are listed here.

   

    

1. Select a pre-defined resource size or customize your own from the options listed:

   a. **Small**: File data is under 100 GB. Driver memory (GB): 2GB, Driver cores: 1 vCPU, Number of executors: 1, Executor cores: 1 vCPU, and Executor memory (GB): 2GB.

   b. **Medium**: File data is between 100 GB - 500 GB. Driver memory (GB): 4GB, Driver cores: 2 vCPU, Number of executors: 2, Executor cores: 2 vCPU, and Executor memory (GB): 4GB.

   c. **Large**: File data is above 500 GB. Driver memory (GB): 8GB, Driver cores: 4 vCPU, Number of executors: 4, Executor cores: 4 vCPU, and Executor memory (GB): 8GB.

   d. **Custom**: Configure the five (5) resources for your job based on your needs.

1. In the **Select file(s)** tab, browse and select your remote file(s) from your connected bucket(s) by clicking **Select remote files**.
1. From the **Bucket** drop-down, select the bucket from where you want to ingest the data.
1. Select the required file type based on the source data. The available options are CSV and Parquet.
1. From the source directory, select the source data files to be ingested and click **Next**.

    You can apply the configuration for **Header**, **Encoding**, **Escape character**, **Field delimiter**, and **Line delimiter** for the CSV files.
    {: note}

1. View the   selected files and the corresponding file previews in the **File(s) selected** and **File preview** tabs. File preview enables to preview first 10 rows of the selected source file.
1. In the **Target** tab, select the target catalog from the **Select catalog** list.

   The selected catalog must be active to perform an ingestion job.
   {: note}

1. Select one of the schema options:
   1. **Existing schema**: To ingest source data into an existing schema. Corresponding target schemas are listed in the **Select schema** dropdown.
   2. **New schema**: Enter the target schema name in **Schema name** to create a new schema from the source data.
1. Select the corresponding **Target table** options based on the selection in step 12.
   1. **Existing table**:To ingest source data into an existing table. Corresponding target tables are listed in the **Select table** dropdown.
   2. **New table**: Enter the target table name in **Table name** to create a new table from the source data.
1. Click **Next**.
1. Validate the details in the summary page. Click **Ingest**.

To enable your Spark application and ingestion to work with the {{site.data.keyword.lakehouse_short}} catalog and storage, you must have `MetastoreAdmin`, and `DataAccess` roles in the Service access and `Administrator` role in the Platform access, see [Managing IAM access for watsonx.data](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-iam).
 Without `Metastore admin` privilege, you cannot ingest data to storage using Native Spark engine. For more information about the Spark configuration, see [Working with the watsonx.data catalog and storage](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-smbit_nsp#view_smbit_nsp).
{: note}

Ingesting data

1. Log in to {{site.data.keyword.lakehouse_full}} console.
2. From the navigation menu, select **Data manager**.
3. Click the **Ingest data** module. The **Ingest data** window opens.
4. Select one of the storage options to proceed to the next page:

   a. **Local System**: To select your files from your local system.

   b. **Storages**: To select remote file(s) from your connected S3 compatible bucket(s).

5. Follow the steps to ingest data from **Local system**:

   i. Select a bucket from the **Select storage** drop-down. (You can also add a new storage bucket by clicking **Add +**).

   ii. Select the required file type based on the source data. The available options are CSV, Parquet, and JSON.

   iii. Select the files to be ingested from the **All files** tab. Selected files are listed in the **Files selected** tab. You can also preview the details of the selected files in the **File details** pane.

   iv. In the **Target table** pane, select the target catalog from the **Select catalog** list. The selected catalog must be active to perform an ingestion job.

   v. Choose one of the schema options:

      1.  Existing schema: To ingest source data into an existing schema. Search or select a target schema listed in the **Select schema or enter new schema name (New)** dropdown.

      2. New schema: Enter the target schema name in the **Select schema or enter new schema name (New)** to create a new schema from the source data.

   vi. Select the corresponding Target table options based on the selection (above).

      1. Existing table:To ingest source data into an existing table. Search or select a target table listed in the **Select table or enter new table name** dropdown.

      2. New table: Enter the target table name in the **Select table or enter new table name** to create a new table from the source data.

   vii. If required, modify the auto-generated ingestion Job ID in the **Job Details**.

   viii. Select the IBM Analytics Engine (Spark) from the **Select engine** list. The registered Spark engines are listed here.

   xi. Click **Done**. The submitted ingestion job can be found in the **Ingestion history** tab of the **Data manager** page.

6. Follow the steps to ingest data from **Storages**:

   i. Select a bucket from the **Select storage** drop-down. (You can also add a new storage bucket by clicking **Add +**).

   ii. Select the required file type based on the source data. The available options are CSV, Parquet, and JSON.

   iii. Select the files to be ingested from the **All files** tab. Selected files are listed in the **Files selected** tab. You can also preview the details of the selected files in the **File details** pane.

   iv. In the **Target table** pane, select the target catalog from the **Select catalog** list. The selected catalog must be active to perform an ingestion job.

   v. Choose one of the schema options:

      1.  Existing schema: To ingest source data into an existing schema. Search or select a target schema listed in the **Select schema or enter new schema name (New)** dropdown.

      2. New schema: Enter the target schema name in the **Select schema or enter new schema name (New)** to create a new schema from the source data.

   vi. Select the corresponding Target table options based on the selection (above).

      1. Existing table:To ingest source data into an existing table. Search or select a target table listed in the **Select table or enter new table name** dropdown.

      2. New table: Enter the target table name in the **Select table or enter new table name** to create a new table from the source data.

   vii. If required, modify the auto-generated ingestion Job ID in the **Job Details**.

   viii. Select the IBM Analytics Engine (Spark) from the **Select engine** list. The registered Spark engines are listed here.

   xi. Click **Done**. The submitted ingestion job can be found in the **Ingestion history** tab of the **Data manager** page.

## Limitations
{: #limits001}

Following are some of the limitations of Spark ingestion:

- Spark ingestion supports only source data files from object storage bucket. Local files are not supported.
- The default buckets in watsonx.data are not exposed to Spark engine. Hence, iceberg-bucket and hive-bucket are not supported for source or target table. Users can use their own MinIo or S3 compatible buckets that are exposed and accessible by Spark engine.
