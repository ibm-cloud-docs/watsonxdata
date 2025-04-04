---

copyright:
  years: 2022, 2025
lastupdated: "2025-03-24"

keywords:  query, engine, infrastructure

subcollection: watsonxdata

content-type: tutorial
account-plan: paid
completion-time: 0.5h

---

{{site.data.keyword.attribute-definition-list}}


{:step: data-tutorial-type="step"}
{:shortdesc: .shortdesc}

# Adding storage and querying data
{: #tutorial_prov_custbckt1}
{: toc-content-type="tutorial"}
{: toc-completion-time="0.5h"}

In this tutorial, you learn to add a storage that you own and explore how the {{site.data.keyword.lakehouse_short}} service interacts with the data you bring in.
{: shortdesc}

**Sample Scenario** : Your team is working on developing an automated data pipeline that requires querying data from the data bucket that you have. Your manager requests you to retrieve data from the data bucket by using the {{site.data.keyword.lakehouse_short}} instance.

For this scenario, you must create the Presto query engine, establish connection with the storage, ingest data to the data bucket and display the result in {{site.data.keyword.lakehouse_short}} instance.


## Objective
{: #custbckt_obj1}

* Creating infrastructure within the {{site.data.keyword.lakehouse_short}} service.

* Establishing connection with the customer data bucket.

* Querying from the bucket

![Workflow diagram](images/customerbucket.svg){: caption="Workflow diagram" caption-side="bottom"}

## Before you begin
{: #custbckt_byb1}

This tutorial requires:

* Subscription of {{site.data.keyword.lakehouse_short}} on cloud.
* The configuration details of data bucket that you bring in. This is required for establishing connetion with the {{site.data.keyword.lakehouse_short}}.
* Provision {{site.data.keyword.lakehouse_short}} service instance




## Adding the storage that you own and ingesting data
{: #hp_ingest1}
{: step}

In this section of the tutorial, you learn how to register the storage bucket that you bring and add data to it.

1. To add a storage bucket that you own, see [Adding a storage-catalog pair](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-reg_bucket).
1. You can use the **Create table** option from the **Data manager** page to load local or external sources of data files to create tables. You can also ingest large files by using the CLI. See more [Creating an ingestion job by using the configuration file](/docs/watsonxdata?topic=watsonxdata-create_ingestconfig){: external}.


## Querying data
{: #hp_qury1}
{: step}

In this section of the tutorial, you learn how to navigate to the **Query workspace**, and create SQL queries to query your data from the bucket.

To run SQL query, do the following steps:

1. From the navigation menu, select **SQL**. The **Query workspace** page opens.
2. Select the Presto (Java) engine from the **Engine** drop-down.
3. Select a catalog, for example, **default** schema, and a table, for example, **order_detail**, to run the query.
4. Click the overflow menu and select the required query.
   * For a catalog and schema, you can run the **Generate Path** query.
   * For a table, you can run the **Generate path**, **Generate SELECT**, **Generate ALTER**, and **Generate DROP** query.
   * For a column, you can run the **Generate path**, **Generate SELECT**, and **Generate DROP** query.

   Consider the following sample query to view the details from the table:

   Example:

   ```bash
   SELECT * FROM "iceberg-beta"."default"."order_detail" LIMIT 10;
   ```
   {: codeblock}

5. Click **Run on** to run the query.
6. Select the **Result set** or **Details** tab to view the results. If required, you can save the query.
7. Click **Saved queries** to view the saved queries.
8. Click [**Explain**](/docs/watsonxdata?topic=watsonxdata-explain_sql_query){: external} to view the logical or distributed plan of execution for a specified SQL query.
