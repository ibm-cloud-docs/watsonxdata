---

copyright:
  years: 2022, 2024
lastupdated: "2024-08-02"

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

# Retrieving query information from QHMM data
{: #ret_qhmm}

You can configure {{site.data.keyword.lakehouse_short}} to store the diagnostic data such as queries history and query event-related information of the Presto engine (Presto) in a storage bucket in {{site.data.keyword.lakehouse_short}} using the **Query monitoring** page. You can retrieve the history files to analyze, debug or monitor the queries. from the Query workspace.
{: shortdesc}

## Procedure
{: #ret_pr_qhmm}



1. Add storage to store the QHMM data. You can use the default storage or bring your own bucket.

1. To know about default storage, see [Configure query monitoring]({{site.data.keyword.ref-quick_start-link}}#qs_montr){: external}.

1. To use your own storage for QHMM data :

    a. Register the storage, see [Adding a storage-catalog pair]({{site.data.keyword.ref-reg_bucket-link}}){: external}. QHMM supports only the Apache Hive catalog.

    b. Associate the storage with a query engine (Presto). For details, see [Associating a catalog with an engine]Configure Query monitoring. For details, see Query monitoring.

    c. Configure Query monitoring. Select the storage bucket that you registered to store QHMM data. For details, see [Query monitoring]({{site.data.keyword.ref-qhmm-link}}){: external}.

    You can also register the storage (that you bring in) at the time of configuring the Quick start wizard. For more information, see [Configure query monitoring]({{site.data.keyword.ref-quick_start-link}}#qs_montr){: external}.

1. From the navigation menu, select **Query workspace**.
1. Select the engine from **Engine** list and identify the catalog that you created to store the QHMM data.
1. You can view the queries history and query event-related information of the Presto engine inside the tables within the catalog. Run queries to analyse the data.
