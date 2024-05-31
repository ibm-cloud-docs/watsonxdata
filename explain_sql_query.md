---

copyright:
  years: 2022, 2024
lastupdated: "2024-05-31"

keywords: watsonxdata, graphical representation, explain sql statement, sql editor, sql query

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

# About Visual Explain
{: #explain_sql_query}

The visual explain feature in {{site.data.keyword.lakehouse_full}} shows the execution plan for a specified SQL query. This feature also validates the SQL query. The output results can be visualized in different formats, which can be rendered into a graph or a flow chart. Data exchange happens between single or multiple nodes within a fragment. Each fragment has a set of data that is distributed between the nodes.
{: shortdesc}

With this visual explain feature, you can run the query and show the output in a distributed environment. You can output the results in different formats. When queries are run, they scan through the database. The queries retrieve table metadata to fetch the correct output.

With this visual explain feature, you can visualize the query in a graphical representation. When a query is run in the SQL editor and selects the **Explain** option, {{site.data.keyword.lakehouse_short}} uses an EXPLAIN SQL statement on the query to create a corresponding graph. This graph can be used to analyze, fix, and improve the efficiency of your queries by saving time and cost.

To view the execution plans for a query that is run in {{site.data.keyword.lakehouse_short}} SQL editor, follow the steps:

1. In the **Query workspace** page, enter the query and click **Run on starter** to get the results.
1. Click **Explain** on the screen to visualize the graphical representation of the query.

On the **Explain** window, click a stage to view the details on the side window. The details of each stage that is displayed are the estimate values for rows, CPU, memory, and network.
