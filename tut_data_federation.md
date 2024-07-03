---

copyright:
  years: 2022, 2024
lastupdated: "2024-07-03"

keywords: Data, federation,

subcollection: watsonxdata

content-type: tutorial
account-plan: paid
completion-time: 0.25h
---

{{site.data.keyword.attribute-definition-list}}

{:shortdesc: .shortdesc}
{:step: data-tutorial-type="step"}



# Connecting and Querying across multiple data sources
{: #Db2tutorial_join_data}
{: toc-content-type="tutorial"}
{: toc-completion-time="0.25h"}


This tutorial guides you through the process of using federated queries to analyze sales data for a fictional Great Retail Company, which is stored in multiple locations.
{: shortdesc}

## Introduction
{: #Db2intro}

### Data federation overview
{: #Db2intro1}

Data federation is a software process that enables several databases to work together. It allows you to mix data from multiple sources to get insights. It allows you to access all of your data across numerous dispersed databases with a single query.

### Presto (Java) engine's data federation capability
{: #Db2intro2}

The Presto (Java) engine's federated query functions allows organizations to effortlessly mix data from several sources, including current databases and new data in {{site.data.keyword.lakehouse_full}}.
By leveraging the capability of watsonx.data to integrate with Presto (Java), your business can now seamlessly combine and analyze data across various sources, gaining deeper insights. This streamlined approach not only enhances operational efficiency but also empowers decision-makers with timely and accurate data-driven insights.

### Use Case Scenario
{: #Db2intro3}

Analyzing purchasing methods across multiple data sources
: The objective of this use case is to analyze the purchasing methods associated with the largest orders.
The sales data is available in Db2. A portion of this data is moved to Iceberg tables within watsonx.data. The sales data is now in two places - Db2 and watsonx.data and you need to perform a Presto (Java) query from both Db2 and Iceberg to analyze the data, aiming to identify the purchasing method that is linked to the largest orders.



## Objective
{: #Db2ibmbckt_obj1}

* Registering your Db2 data source with watsonx.data
* Moving part of sales data from Db2 to watsonx.data
* Running query to retrieve insights


## Before you begin
{: #Db2ibmbckt_bfb1}

This tutorial requires:

* Subscription of {{site.data.keyword.lakehouse_short}} on cloud.
* Db2 database with `GOSALESDW` data
* Credentials of Db2 database

## Registering your Db2 data source
{: #db2ibmbckt_stp1}
{: step}

Register the Db2 data source (that has `GOSALESDW` data in it) with {{site.data.keyword.lakehouse_short}} instance.
{: shortdesc}

To register your Db2 data source, see [IBM Db2](watsonxdata?topic=watsonxdata-reg_database#db2){: external}. Use the following details when you register the Db2 data source.

* Database name : Enter the database name as `BLUDB`.
* Hostname : Enter the hostname as `db2w-sucqakq.us-south.db2w.cloud.ibm.com`
* Username : `db2inst`
* Password : `Usertutorials1!`
* Port : `50001`


## Associating Db2 with Presto (Java) engine
{: #db2ibmbckt_stp2}
{: step}

After you register the Db2 database, you must associate the catalog with the Presto (Java) engine. For more information, see [Associating a catalog with an engine](watsonxdata?topic=watsonxdata-asso-cat-eng){: external}.


## Copying data from Db2 database to Iceberg
{: #db2ibmbckt_stp3}
{: step}

After you associate the catalog with the engine, copy data (a single table) from Db2 to Iceberg. To do that, complete the following steps:
{: shortdesc}

1. From the navigation menu, select **Data Manager**. Create a schema inside `Iceberg_data` catalog. For more information on how to create a schema, see [Creating schema](watsonxdata?topic=watsonxdata-create_schema){: external}.
1. From the navigation menu, select **Query Workspace**.
1. Write a query to copy the data from`GOSALESDW` table present in the Db2 database and create a new table (here `demo_table`) inside `Iceberg` catalog.

   Example query:

   ```bash
   CREATE TABLE"iceberg_data"."demo_schema"."demo_table" AS SELECT * FROM "demo_catalog"."gosalesdw"."sls_sales_fact"
    ```
    {: codeblock}

1. Click the **Run on starter** button to run the query.
6. Refresh `Iceberg_data` catalog to view the new table `demo_table`.

## Data federation
{: #db2ibmbckt_step4}
{: step}

Now, the sales data is split between Db2 and Iceberg catalogs. You can run query from both Db2 and Iceberg to analyze the data and generate insights about the purchasing methods that are associated with the largest orders. To do that:



2. From the **Query Workspace**, run the following query to understand which purchasing method is associated with the largest orders.

   Example query:

   ```bash
   	select pll.product_line_en as product,
            md.order_method_en as order_method,
            sum(sf.quantity) as total
            from
            "demo_catalog"."gosalesdw"."sls_order_method_dim" as md,
            "demo_catalog"."gosalesdw"."sls_product_dim" as pd,
            "demo_catalog"."gosalesdw"."sls_product_line_lookup" as pll,
            "demo_catalog"."gosalesdw"."sls_product_brand_lookup" as pbl,
            "iceberg_data"."demo_schema"."demo_table" as sf
            where
            pd.product_key = sf.product_key
            and md.order_method_key = sf.order_method_key
            and pll.product_line_code = pd.product_line_code
            and pbl.product_brand_code = pd.product_brand_code
            group by pll.product_line_en, md.order_method_en
            order by product, order_method;
    ```
    {: codeblock}

5. Click the **Run on** button to run the query.
6. Select the **Result set** or **Details** tab to view the result.

With these capabilities, your enterprise can drive smarter operations, optimize purchasing methods, and ultimately improve overall business performance.
