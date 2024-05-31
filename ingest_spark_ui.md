---

copyright:
  years: 2022, 2024
lastupdated: "2024-05-31"

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

# Ingesting data by using Spark
{: #ingest_spark_ui}

You can ingest data into {{site.data.keyword.lakehouse_full}} by using {{site.data.keyword.iae_full_notm}} (Spark) through the web console.
{: shortdesc}

## Before you begin
{: #spk_ing}

* You must have the **Administrator** role and privileges in the catalog to do ingestion through the web console.
* Add and register {{site.data.keyword.iae_full_notm}} (Spark). See [Registering an engine](watsonxdata?topic=watsonxdata-reg_engine).
* Add buckets for the source data files and target catalog. See [Adding a bucket-catalog pair](watsonxdata?topic=watsonxdata-reg_bucket).
* Optionally, you can create a schema in the catalog for the target table. See [Creating schemas](watsonxdata?topic=watsonxdata-create_schema).
* Optionally, you can also create a target table in the schema. See [Creating tables](watsonxdata?topic=watsonxdata-create_table).

## Ingesting data
{: #spk_ingest_data}

1. Log in to {{site.data.keyword.lakehouse_full}} console.
1. From the navigation menu, select **Data manager**.
1. Select the **Ingestion jobs** tab and click **Create ingestion job**. The **Ingest data** window opens with an auto-generated job ID.
1. If required, modify the auto-generated ingestion job ID in the **Enter job ID** field.
1. Select a registered IBM Analytics Engine (Spark) from the **Select engine** list.

   <!-- 1. Configure Spark driver cores, executor cores, and memory resources. Click **Next**. -->

    <!-- For IBM Cloud, the Spark driver, executor vCPU and memory combinations must be in a 1:2, 1:4, or 1:8 ratio. The default configuration values are filled. See [Default limits and quotas for Analytics Engine instances](https://cloud.ibm.com/docs/AnalyticsEngine?topic=AnalyticsEngine-limits).
    {: note} -->

1. Select size (**Small**, **Medium**, **Large**, or **Custom**) for Spark engine resource configurations based on the size of source data that is getting ingested. If you want to customize the configurations, select  **Custom**, and configure your own Spark driver cores, executor cores, and memory resources.
1. In the **Select file(s)** tab, click **Select remote files**.
1. From the **Bucket** drop-down, select the bucket from where you want to ingest the data.
1. Select the required file type based on the source data. The available options are CSV and Parquet.
1. From the source directory, select the source data files to be ingested and click **Next**.

    You can apply the configuration for **Header**, **Encoding**, **Escape character**, **Field delimiter**, and **Line delimiter** for the CSV files.
    {: note}

1. View the   selected files and the corresponding file previews in the **File(s) selected** and **File preview** tabs. File preview enables to preview first 10 rows of the selected source file.
1. In the **Target** tab, select the target catalog from the **Select catalog** list.
1. Select one of the schema options:
   1. **Existing schema**: To ingest source data into an existing schema. Corresponding target schemas are listed in the **Select schema** dropdown.
   2. **New schema**: Enter the target schema name in **Schema name** to create a new schema from the source data.
1. Select the corresponding **Target table** options based on the selection in step 12.
   1. **Existing table**:To ingest source data into an existing table. Corresponding target tables are listed in the **Select table** dropdown.
   2. **New table**: Enter the target table name in **Table name** to create a new table from the source data.
1. Click **Next**.
1. Validate the details in the summary page. Click **Ingest**.

## Limitations
{: #limits001}

Following are some of the limitations of Spark ingestion:

- Spark ingestion supports only source data files from object storage bucket. Local files are not supported.
- The default buckets in watsonx.data are not exposed to Spark engine. Hence, iceberg-bucket and hive-bucket are not supported for source or target table. Users can use their own MinIo or S3 compatible buckets that are exposed and accessible by Spark engine.
