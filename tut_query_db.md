---

copyright:
  years: 2022, 2024
lastupdated: "2024-04-03"

keywords: provisioning, query, engine, infrastructure

subcollection: watsonxdata

content-type: tutorial
account-plan: paid
completion-time: 0.5h

---

{{site.data.keyword.attribute-definition-list}}


{:step: data-tutorial-type="step"}
{:shortdesc: .shortdesc}

# Getting started with your query engine
{: #tutorial_get_strt}
{: toc-content-type="tutorial"}
{: toc-completion-time="0.5h"}

<!-- / Getting familiarized with Presto query engine -->
<!-- Exploring Presto functionality for a first time user -->

After successfully provisioning the Presto engine, kickstart your {{site.data.keyword.lakehouse_short}} experience by exploring the capabilities of Presto by running test queries, creating your first schema, and tables.
{: shortdesc}

In this tutorial, you learn to execute some test queries to understand the capabilities of Presto and create your first schema to establish a foundational structure for organizing your data. When your schema is in place, you can proceed to create your table. Tables are essential components for storing and organizing data.


**Sample Scenario** : To understand:
* Querying tables by using Presto in {{site.data.keyword.lakehouse_short}}
* About the data available for kick start
* To learn how to create schemas and tables to store, organize and query data.

<!-- For this scenario, you must create the Presto query engine, establish connection, read data from the data bucket and display the result in {{site.data.keyword.lakehouse_short}} instance.

This scenario assumes that you already have a data bucket that is associated with data for querying.
{: note} -->


## Objective
{: #gtstrd_obj}

* Running test queries
* Creating your first schema and table


## Before you begin
{: #gtstrtd_byb}

This tutorial requires:

* Subscribe to {{site.data.keyword.lakehouse_short}} on IBM Cloud.
* Provision your {{site.data.keyword.lakehouse_short}} instance. For more information, see [Trial experience](watsonxdata?topic=watsonxdata-tutorial_hp_intro){: external}.


## Running test queries
{: #gtstrtd_stp1}
{: step}

This section of the tutorial describes how to use the **Query workspace**, and run test queries to familiarize with the working of the Presto engine.

To run the SQL query, do the following steps:

1. From the navigation menu, select **SQL**. The **Query workspace** page opens.
2. Select the Presto engine from the **Engine** list.
3. Go to **System and benchmarking data**. {{site.data.keyword.lakehouse_short}} provides default catalogs **tpcds**, and **tpch**. These catalogs provide auto-generated data for benchmarking. You can also use it for running sample queries and data.
4. Select a schema from the **tpch** catalog (for example, `Tiny`) and then select a table, for example, `Customer`. Click the overflow menu to select **Generate Path**, or **Generate SELECT**.
4. Select **Generate Select** and select a limit, for example 100.
5. Click **Run on** to run the query.
6. Select the **Result set** or **Details** tab to view the results. If required, you can save the query.


## Saving data
{: #gtstrtd_stp2}
{: step}

1. From the navigation menu, select **Data manager**. The **Data manager** page opens.
2. Select the **iceberg_data** catalog. The catalog is available by default.
3. Click **Create**. Select **Create schema** to create a schema under the **iceberg_data** catalog. For more information, see [Creating schema](watsonxdata?topic=watsonxdata-create_schema){: external}.
4. Give your schema a name, for example `new_schema`.
4. To store data, you must create tables inside the schema. Use one of the following options to create a table:

* Option 1: You can create a table (with the default data that is available in the **tpcds** catalog) by running an SQL query.

     a. Go to the **Query workspace** page.

     b. Run **Create table** query. A sample query is shown:

    ```bash
      CREATE TABLE IF NOT EXISTS
      "iceberg_data"."new_schema"."new_table"
      AS SELECT * FROM "tpcds"."sf1"."catalog_returns"
      LIMIT
       100;
    ```
    {: codeblock}

    The SQL query creates a table named, `new_table` by using `new_schema`, within the `iceberg_data catalog`. It also loads data from the `catalog_returns` table, which uses the `sf1` schema in the `tpcds` catalog.

    You can go to the **iceberg_data** catalog and run a select query statement to verify if `new_table` has data in it.

* Option 2: You can create a table by uploading your own data (.csv, parquet, .json, .txt format).

     a. Go to the **Data manager** page.

     b. You can create table with your data in .csv, parquet, .json, .txt formats. To do that, see [Creating table](watsonxdata?topic=watsonxdata-create_schema){: external}.

    You can go to the **Query workspace** page. Select the newly created table from the **iceberg_data** catalog and run a select query statement to verify if the table has data in it.

## Querying data from the table created
{: #gtstrtd_stp3}
{: step}

You can run a **Generate SELECT** query from the new table that is created within the **iceberg_data** catalog. To do that:

1. From the navigation menu, go to the **Query workspace** page.
2. Select the table, `new_table` within the schema, `new_schema`inside the catalog `iceberg_data`.
3. Select **Generate SELECT**.
4. Edit the limit to 100 as shown in the example:
    ```bash
      SELECT * FROM
      "iceberg_data"."new_schema"."new_table"
      LIMIT
       100;
    ```
    {: codeblock}

5. Click the **Run on** to run the query.
6. Select the **Result set** or **Details** tab to view the results. You can also save the query.
