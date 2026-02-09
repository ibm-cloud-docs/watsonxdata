---

copyright:
  years: 2022, 2025
lastupdated: "2026-02-09"

keywords: watsonxdata, query history

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

# Query history
{: #query_history}

A query history audits all current and past queries that run across existing engines in {{site.data.keyword.lakehouse_full}}.
{: shortdesc}

The page provides a consolidated and searchable record of query execution activity, helping users monitor performance, review workload patterns, and understand resource consumption across engines.


## What you can view in Query history
{: #query_history1}

The **Query history** page provides the following key information for every query:

* Query ID
* Query text
* State (such as Running, Finished, Failed)
* Engine and Engine ID
* User
* Source (where the query originated)
* CPU
* Memory (GB)
* Usage (RUs)


Within the **Query history** page, you can:

* **Search** for queries by ID, text, user, or other attributes.
* Refresh the list to load the latest query activity.
* Filter by engine, state, user, or other properties.
* Customize the table by showing or hiding columns.
* Download the full query history as a CSV file.
* Select a specific Query to:
   * View or copy the query statement.
   * Review the logical execution plan.
   * Explore the distributed execution plan.
   * View EXPLAIN ANALYZE information.

* Open queries directly in a workspace.
* Access explain details from the overflow menu for each query.

For more information about exporting and importing query history, see [Exporting and importing the query history]({{site.data.keyword.ref-eximp-q-hist-link}}).
