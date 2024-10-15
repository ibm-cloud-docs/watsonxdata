---

copyright:
  years: 2022, 2024
lastupdated: "2024-10-15"

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


Query History Monitoring and Management (QHMM) is a service that stores and manages the diagnostic data such as, heap dumps, thread dumps, queries history and query event-related information of the Presto(Java) and Presto(C++) engine in a storage bucket. You can retrieve the stored history files for analysis, debugging and monitoring purpose.

QHMM primarily aims to address the issue of data persistence for serviceability data. When the engine restarts or goes offline, there are chances of losing valuable diagnostic data they generate. QHMM resolves the issue by storing such data in object storage solutions like Cloud Object Storage (COS) or Minio buckets. The data is organized in a structured folder hierarchy, making it easily accessible for users to retrieve and analyze.

QHMM allows to retrieve the following diagnostic data:
* Events generated against a running query in Presto, following are the query events:
    * Query created event - event logged when a query is initiated.
    * Split completed event - split correspond to an individual task in a query execution. An event is logged when a split or a task is completed.
    * Query completed event - event logged when a query execution is completed.
    * Query Optimiser event - event logged when the query optimizer is enabled.
* Histories of the queries executed by Presto in the form of a json file.
* Query history table created where user can execute a query to view the histories of the queries executed by Presto.
* Heap dump by using API.



## Related topics
{: #data_qhmm_rel}

* Configuring QHMM, see [Configuring Query monitoring](watsonxdata?topic=watsonxdata-qhmm)

* Managing diagnostic data from user interface, see [Configuring Query monitoring](watsonxdata?topic=watsonxdata-ret_qhmm)

* Managing diagnostic data by manual method, see [Configuring Query monitoring](watsonxdata?topic=watsonxdata-mon_mng)
