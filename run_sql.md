---

copyright:
  years: 2022, 2025
lastupdated: "2025-03-25"

keywords: watsonxdata, sql queries, query workspace

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

# Running SQL queries
{: #run_sql}

SQL is a standardized language for defining and manipulating data in a relational database. You can use the **Query workspace** interface in {{site.data.keyword.lakehouse_full}} to run SQL queries and scripts against your data.
{: shortdesc}

The **Query workspace** has the following components:

- **Engine**: To select an engine and view the associated catalogs.

- **Filter for tables**: To search the tables and columns.

- **Worksheet**: To write SQL queries.

- {{site.data.keyword.lakehouse_short}} provides pre-defined **Sample and benchmarking data**, such as **tpch** and **tpcds**, to test the performance of a database system under controlled conditions. It also provides **System monitoring data** that uses **jmx** and **system** metrics to collect data about the system's health and performance during benchmark testing to understand how the system responds to the workload. **Sample and benchmarking data**, **tpch** and **tpcds** can only be queried using the Presto engines.

- **Saved worksheets**: To view the saved queries.

- **Sample worksheets**: To run predefined sample queries to analyze the performance between different engines on the same data set.

The **Query workspace** page provides basic options to **undo, redo, cut, copy, paste, save, clear,** and **delete**.

**Format selection** option is enabled only when an SQL statement in a query worksheet is selected. The **Format worksheet** option formats all the content in the worksheet. **Comment selection** is used to explain sections of SQL statements.

The **Delete** option is enabled only after an SQL query is saved.

To run the SQL queries, do the following steps:

1. Log in to the {{site.data.keyword.lakehouse_short}} console.
1. From the navigation menu, select **SQL**.  The **Query workspace** page opens.
1. Select an engine from the **Engine** drop-down.
1. Select the catalog, schema, table, or column in which you want to run the query.
1. Click the overflow menu and select the required query.

   * For a catalog and schema, you can run the **Generate Path** query.
   * For a table, you can run the **Generate path**, **Generate SELECT**, **Generate ALTER**, and **Generate DROP** query.
   * For a column, you can run the **Generate path**, **Generate SELECT**, and **Generate DROP** query.

1. Select the **Catalog** and corresponding **Schema** from the drop-down on top of the worksheet to run queries for all tables within the schema without having to specify the path (`<catalog>.<schema>`) for every queries.

1. Click the **Save** icon to save the query. A **Save query** confirmation dialog appears.
1. Click **Save**.
1. Click the **Run** button to run the query. Using **Run to cursor** or **Run from cursor**, you can run queries from or until your cursor position.

   You can cancel a query while running single or multiple queries. Additionally, you can remove a query either after canceling it or once its execution is completed. These options are available for each respective query in the **Worksheet results** view.
   {: note}

1. Select **Result set** or **Details** tab to view the results. You can export the result as a csv file using **Export to CSV** icon.
1. Click **Saved queries** to view the saved queries.
1. Click [**Explain**]({{site.data.keyword.ref-explain_sql_query-link}}) to view the logical or distributed plan of execution for a specified SQL query.

## Related API
{: #query_api}

For information on related API, see
* [Execute a query](https://cloud.ibm.com/apidocs/watsonxdata-software#create-execute-query)
