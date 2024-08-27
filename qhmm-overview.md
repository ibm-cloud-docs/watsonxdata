---

copyright:
  years: 2022, 2024
lastupdated: "2024-08-27"

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

QHMM primarily aims to address the issue of data persistence for serviceability data. When the engine restarts or go offline, there are chances of losing valuable diagnostic data they generate. QHMM resolves the issue by storing such data in object storage solutions like COS (Cloud Object Storage) or Minio buckets. The data is organized in a structured folder hierarchy, making it easily accessible for users to retrieve and analyze.

QHMM allows to retrieve the following diagnostic data:
* Events generated against a running query in presto, following are the query events:
    * Query created event - event logged when a query is initiated.
    * Split completed event - split correspond to an individual task in a query execution. An event is logged when a split or a task is completed.
    * Query completed event - event logged when a query execution is completed.
    * Query Optimiser event - event logged when the query optimizer is enabled.
* Tables and views that hold relevant information related to query event.
* Histories of the queries executed by Presto in the form of a json file.
* Query history table created where user can execute a query to view the histories of the queries executed by Presto.


## Data organization
{: #data_qhmm}

You can enable or disable the QHMM service for your {{site.data.keyword.lakehouse_short}} instance. If you enable the QHMM service, you must specify the storage to be used for storing the query data.
{{site.data.keyword.lakehouse_short}} allows using the default storage, `wxd-system` to store the QHMM data or register your own storage (BYOB). To use BYOB, register your bucket in watsonx.data and configure it to use as QHMM storage. You can do that either from Quick start or from {{site.data.keyword.lakehouse_short}} console page. For more information, see [Retrieving query information from QHMM data](watsonxdata?topic=watsonxdata-ret_qhmm){: external}.

You can choose the QHMM storage (default QHMM bucket or your own bucket) from:

* Quick start wizard (see [Configure query monitoring](watsonxdata?topic=watsonxdata-quick_start#qs_montr){: external})
* {{site.data.keyword.lakehouse_short}} console page (see [Query monitoring](watsonxdata?topic=watsonxdata-qhmm){: external})

You can retrieve the history files to analyze, debug, or monitor the queries. From the Query workspace see, [Retrieving query information from QHMM data](watsonxdata?topic=watsonxdata-ret_qhmm).


QHMM maintains a structured folder hierarchy within the chosen object storage solution to store data efficiently. The structure is as follows:

`<base_path>/ <wxdInstanceID>/ <engine or service type>/ <engine or service ID>/ <recordtype>/ dt=<dd-MM-yyyy> <records>`

* `<base_path>` : Default base_path is qhmm and you can change the path from the QHMM configuration page.
* `<wxdInstanceID>`: A unique identifier for the instance.
* `<engine or service type>`: The type of engine sending the data.
* `<engine or service ID>`: A unique identifier for the engine.
* `date<dd-MM-yyyy>`: The date on which the data is recorded.
* `<recordtype>`: The type of diagnostic data (e.g., query history, query events, dumps).
* `<records>`: The actual data records stored.

To store query history details, one more folder is added: `<base_path>/ <wxdInstanceID>/ <engine or service type>/ <engine or service ID>/ <recordtype>/ dt=<dd-MM-yyyy> <user> <records>`.

* `<user>`: The username of the person who executed the query.


## Related topics
{: #data_qhmm_rel}

* Configuring QHMM, see [Query monitoring](watsonxdata?topic=watsonxdata-qhmm)

* Diagnostics Data Retrieval for Presto Engine Serviceability, see [Retrieving query information from QHMM data](watsonxdata?topic=watsonxdata-ret_qhmm)
