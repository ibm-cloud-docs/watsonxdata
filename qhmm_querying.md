---

copyright:
  years: 2022, 2024
lastupdated: "2024-10-25"

keywords: watsonxdata, qhmm

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

# Managing diagnostic data from user interface
{: #ret_qhmm}

You can configure {{site.data.keyword.lakehouse_short}} to store the diagnostic data such as queries history and query event-related information of the Presto engine (Presto) in a storage bucket in {{site.data.keyword.lakehouse_short}} using the **Query monitoring** page. You can retrieve the history files to analyze, debug or monitor the queries from the Query workspace.
{: shortdesc}

## Procedure
{: #ret_pr_qhmm}


1. From the navigation menu, select **Query workspace**.
1. Select the engine from **Engine** list and identify the Hive catalog that you created to store the QHMM data.
1. You can view the queries history and query event-related information of the Presto engine inside the tables within the catalog. Run queries to analyse the data.
1. The following tables are available by default:

    query_event_raw : Includes the raw data of query events in JSON format. To view the entire event data, use the following query:

    SELECT*FROM`<catalog>.<schema>`.query_event_raw;

    query_history : Includes the query History data. To view the entire Query History data, use the following query:

    SELECT*FROM`<catalog>.<schema>`.query_history;

    table_stats_information_memory : Includes the memory related information. To view the memory related information, use the following query:

    SELECT*from`<catalog>.<schema>`.table_stats_information_memory;
