---

copyright:
  years: 2022, 2024
lastupdated: "2024-07-03"

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

- **Data objects**: To view the engines, catalogs, schemas, tables, and columns.

- **Engine**: To select an engine and view the associated catalogs.

- **Saved queries**: To view the saved queries.

- **Worksheet**: To write SQL queries.

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

1. Click the **Save** icon to save the query. A **Save query** confirmation dialog appears.
1. Click **Save**.
1. Click the **Run** button to run the query. Using **Run to cursor** or **Run from cursor**, you can run queries from or until your cursor position.
1. Select **Result set** or **Details** tab to view the results. You can export the result as a csv file using **Export to CSV** icon.
1. Click **Saved queries** to view the saved queries.

   SQL statements within worksheets can be shared with all users who have access to the instance. These statements could be viewed, edited, or deleted by any of these users.
   {: note}

1. Click [**Explain**](watsonxdata?topic=watsonxdata-explain_sql_query) to view the logical or distributed plan of execution for a specified SQL query.
