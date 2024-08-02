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

# QHMM
{: #ovrvw_qhmm}

Query History Monitoring and Management (QHMM) is a service that stores and manages the diagnostic data such as, queries history and query event-related information of the Presto(Java) and Presto(C++) engine in a storage bucket. You can retrieve the stored history files for analysis, debugging and monitoring purpose.

You can enable or disable the QHMM service for your {{site.data.keyword.lakehouse_short}} instance. If you enable the QHMM service, you must specify the storage to be used for storing the query data.
{{site.data.keyword.lakehouse_short}} allows using the default storage, `wxd-system` to store the QHMM data or register your own storage (BYOB). To use BYOB, register your bucket in watsonx.data and configure it to use as QHMM storage. You can do that either from Quick start or from {{site.data.keyword.lakehouse_short}} console page. For more information, see [Retrieving query information from QHMM data](watsonxdata?topic=watsonxdata-ret_qhmm){: external}.

You can choose the QHMM storage (default QHMM bucket or your own bucket) from:

* Quick start wizard (see [Configure query monitoring](watsonxdata?topic=watsonxdata-quick_start#qs_montr){: external})
* {{site.data.keyword.lakehouse_short}} console page (see [Query monitoring](watsonxdata?topic=watsonxdata-qhmm){: external})

You can retrieve the history files to analyze, debug, or monitor the queries. from the Query workspace (see ([Retrieving query information from QHMM data](watsonxdata?topic=watsonxdata-ret_qhmm){: external})).
