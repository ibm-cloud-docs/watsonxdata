---

copyright:
  years: 2022, 2024
lastupdated: "2024-09-25"

keywords: lakehouse, engine, watsonx.data
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

# Accessing Spark logs for ingestion jobs
{: #ingest_sparklogshistory}

This topic provides the steps required to locate and view Spark logs associated with submitted ingestion jobs within {{site.data.keyword.lakehouse_full}}. By accessing these logs, you can gain valuable insights into the execution details, potential error messages related to the ingestion process, and troubleshooting ingestion jobs.
{: shortdesc}

## Before you begin
{: #ingest_sparklogshistorybyb}

For a **Failed** or **Finished** status, you must start the Spark history server to get the ingestion log details. For more information, see [Accessing the Spark history server](watsonxdata?topic=watsonxdata-wxd_spk_histry).

## Procedure
{: #ingest_sparklogshistoryprcdre}

1. Log in to {{site.data.keyword.lakehouse_short}} console.

2. From the navigation menu, select **Data manager** and click **Ingestion history** tab.

3. Locate the specific ingestion **Job ID** you want to examine.

4. Click on the **Spark log ID** associated with the ingestion job to get log details based on the status of the ingestion job as follows:

   **Starting**: If the ingestion job is in **Starting** status, clicking the **Spark log ID** may not provide immediate details. You might see a message indicating that the application ID is not available yet.

   **Running**: If the job status is **Running**, clicking the **Spark log ID** will generally take you to the Spark UI. You can monitor the ingestion job progress, resource usage, and other details in real-time through this web interface. This Spark UI information will be temporarily available only when the job is in the **Running** status.

   **Failed** or **Finished**: If the job status is **Failed** or **Finished**, clicking the Spark log ID will navigate you to the Spark history UI. This interface provides a summary of the ingestion job execution, including its timeline, resource usage, and any error messages.


   If an ingestion job encountered an issue and failed early in its execution and did not generate a Spark application ID, it is likely that the job did not progress far enough for a Spark log ID to be created. Therefore, the Spark log ID will not be available to provide details about the ingestion process.
   {: note}
