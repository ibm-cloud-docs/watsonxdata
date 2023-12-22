---

copyright:
  years: 2022, 2023
lastupdated: "2023-12-07"

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
* Add a bucket for the target catalog. See [Adding a bucket-catalog pair](watsonxdata?topic=watsonxdata-reg_bucket).
* Create a schema and table in the catalog for the data to be ingested. See [Creating schemas](watsonxdata?topic=watsonxdata-create_schema) and [Creating tables](watsonxdata?topic=watsonxdata-create_table).

## Ingesting data
{: #spk_ingest_data}

1. Log in to {{site.data.keyword.lakehouse_full}} console.
1. From the navigation menu, select **Data manager**.
1. Select the **Ingestion jobs** tab and click **Create ingestion** job.
1. Select **sparkengine** from the **Select engine** menu.
1. Configure **Spark driver** cores, executor cores, and memory resources. Click **Next**.

    For IBM Cloud, the Spark driver, executor vCPU and memory combinations must be in a 1:2, 1:4, or 1:8 ratio. See [Default limits and quotas for Analytics Engine instances](https://cloud.ibm.com/docs/AnalyticsEngine?topic=AnalyticsEngine-limits).
    {: note}

1. Select a source directory from the **Source bucket** menu. Data objects in the source directory are displayed.
1. Select the data objects to be ingested from the source directory. Click **Next**.
     You can apply the configuration for **Encoding**, **Escape character**, **Field delimiter**, and **Line delimiter** for the CSV files.
     {: note}

1. Specify the target details such as **Catalog**, **Schema**, and **Table**.
1. Click **Ingest**.
