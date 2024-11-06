---

copyright:
  years: 2022, 2024
lastupdated: "2024-11-06"

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

For a **Failed** or **Finished** status, you must start the Spark history server to get the ingestion log details. For more information, see [Accessing the Spark history server]({{site.data.keyword.ref-wxd_spk_histry-link}}).

## Procedure
{: #ingest_sparklogshistoryprcdre}

1. Log in to {{site.data.keyword.lakehouse_short}} console.

2. From the navigation menu, select **Data manager** and click **Ingestion history** tab.

3. Click a specific **Job log** to get the details and logs of that ingestion job.

4. Click **Spark application history** to get log details based on the status of the ingestion job as follows:

   **Starting**: If the ingestion job is in **Starting** status, **Spark application history** is disabled.

   **Running**: If the job status is **Running**, clicking **Spark application UI** will generally take you to the Spark UI. You can monitor the ingestion job progress, resource usage, and other details in real-time through this web interface. This Spark UI information will be temporarily available only when the job is in the **Running** status.

   **Failed** or **Finished**: If the job status is **Failed** or **Finished**, clicking **Spark application history** will navigate you to the Spark history UI. This interface provides a summary of the ingestion job execution, including its timeline, resource usage, and any error messages.
