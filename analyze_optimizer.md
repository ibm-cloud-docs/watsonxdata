---

copyright:
  years: 2022, 2025
lastupdated: "2025-10-24"

keywords: lakehouse, bucket, objects, watsonx.data

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

# Managing statistical updates from **Query Optimizer** dashboard
{: #analyze_optimizer}

Once the **Query Optimizer** is successfully activated for the Presto (C++) engine, it enables advanced query performance enhancements and optimization capabilities across multiple catalogs.
{: shortdesc}

The **Query optimizer** allows collecting, storing, and synchronizing table and column statistics for specified tables. These statistics provide essential insights into the data, including row counts, the number of distinct values, minimum and maximum values for each column, and overall data distribution. Only Hive and Iceberg catalogs are supported for the collection of statistics.

The jobs outlined in this topic gather statistics and metadata, and synchronize them with the **Query Optimizer** to support more precise and efficient query planning and execution. Only Hive and Iceberg catalogs are supported for the collection of statistics.

## Viewing Presto (C++) engines
{: #qry-view}

1. From the navigation menu, select **Configurations** and click the **Query Optimizer Manager** tile. The **Query optimizer manager** page opens.
1. Click **Engines** tab. It display the Presto (C++) engines, status, and associated catalogs.

## Collecting statistical information from catalogs
{: #qry-colct}

You can collect, store, and sync catalogs (and tables) associated with the Presto (C++) engine.

1. From the navigation menu, select **Configurations** and click the **Query Optimizer Manager** tile. The **Query optimizer manager** page opens.
1. Click **Catalogs** tab.
1. The **Statistics** tab provides a view of associated catalogs, percentage of tables analyzed relative to the total number of tables within each catalog and the timestamp of the most recent analysis. You can filter the records based on the analysis.
   To do that, click the **Filter** icon. Select the following options and apply the filter condition:

   * No analysis : Select this checkbox to filter catalogs that haven't been analyzed yet.

   * Time since last analysis: Select this checkbox and provide the period (in days or months) to get the list of records processed during the specified period.

1. Click the **Collect statistics** button. The **Collect statistics** page opens with the schemas and tables associated with the Presto (C++) engines. Select the tables and click **Create jobs** to create statistics for tables.

   You can also use the overflow menu next to each catalog on the **Query Optimizer Manager** page to initiate the collection of statistical data for the tables within the selected catalog.
   {: note}

## Viewing the status of the statistical jobs
{: #qry-sts}


1. From the navigation menu, select **Configurations** and click the **Query Optimizer Manager** tile. The **Query optimizer manager** page opens.
1. Click **Catalogs** tab.
2. The **Statistics Jobs** tab provides the list of statistical jobs that you created.

   **Active** : Jobs initiated from the Collect Statistics page that is currently in a Running state is listed here. At any given time, only one job record will appear in the Active state. From the overflow menu, you can :

      * View log : Select this to view the job log for the active record.

      * Add to queue : Select this if you want to move the record to queue.

      * Delete : Select this to delete the record.

      The log information can include the following job status:

      NOTRECEIVED: The system did not receive a call with a given task ID.

      NOTRUN: An error prevented the scheduler from invoking the task’s procedure.

      UNKNOWN: The task began execution, but the scheduler failed to record the outcome due to an unexpected condition.

   **Queued** : If multiple jobs are initiated from the Collect Statistics page, only one will remain in the Active state at a time. All other jobs will be listed and placed in a queue. From the overflow menu, you can select Remove from queue to remove the record from queue.

   **Completed** : The jobs that have completed execution are listed here. From the options available in the overflow menu, you can view the log, add the records to queue, or delete the records.
