---

copyright:
  years: 2022, 2025
lastupdated: "2025-08-25"

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

# Monitoring query performance from Optimizer dashboard
{: #qry-obj}

Once the Query Optimizer is successfully activated for the Presto (C++) engine, it enables advanced query performance enhancements and optimization capabilities across multiple catalogs.
{: shortdesc}

The Query optimizer manager page displays the Presto (C++) engines and their associated catalogs. You can run query analysis on catalogs associated to the engine. It also enables you to track and manage catalog analysis to enhance query performance.

## Viewing Presto (C++) engines
{: #qry-view}

1. From the navigation menu, select **Configurations** and click the **Query Optimizer Manager** tile. The **Query optimizer manager** page opens.
1. Click **Engines** tab. It display the Presto (C++) engines, their status, and their associated catalogs.

## Collecting statistical information from catalogs
{: #qry-colct}

You can do query analysis on catalogs (and tables) associated with the Presto (C++) engine.

1. From the navigation menu, select **Configurations** and click the **Query Optimizer Manager** tile. The **Query optimizer manager** page opens.
1. Click **Catalogs** tab.
1. The **Statistics** tab provides a view of associated catalogs, the percentage of storage data analyzed, and the timestamp of the most recent analysis.
1. Click the **Collect statistics** button. The **Collect statistics** page opens with the schemas and tables associated with the Presto (C++) engines. Select the tables and click **Create jobs** to create statistics for tables.
1. You can also use the overflow menu next to each catalog on the **Query Optimizer Manager** page to initiate the creation of statistical data for the tables within the selected catalog.

## View the status of the statistical jobs
{: #qry-sts}


1. From the navigation menu, select **Configurations** and click the **Query Optimizer Manager** tile. The **Query optimizer manager** page opens.
1. Click **Catalogs** tab.
2. The **Statistics Jobs** tab provides the list statistical jobs that you created.

The table and the associated schema information will be categorized based on the job status Active , Queued and Completed. You can view the logs using the overflow menu.
