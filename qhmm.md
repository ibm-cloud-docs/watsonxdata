---

copyright:
  years: 2022, 2024
lastupdated: "2024-09-12"

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

# Configuring Query monitoring
{: #qhmm}

Query History Monitoring and Management (QHMM) is a service that stores and manages diagnostic data, such as  heap dumps, thread dumps, query history and query event-related information of the Presto engine (Presto) in the default Minio bucket, wxd-system. You can retrieve the history files to analyze, debug or monitor the queries. You can also store the data in your own bucket.
{: shortdesc}

You can enable or disable the QHMM service for your {{site.data.keyword.lakehouse_short}} instance. If you enable the QHMM service, you must specify the storage to be used for storing the query data.
{{site.data.keyword.lakehouse_short}} allows using the default storage, `wxd-system` to store the QHMM data or register your own storage (BYOB). To use BYOB, register your bucket in watsonx.data and configure it to use as QHMM storage. You can do that either from Quick start or from {{site.data.keyword.lakehouse_short}} console page. For more information, see [Retrieving query information from QHMM data](watsonxdata?topic=watsonxdata-ret_qhmm){: external}.

You can choose the QHMM storage (default QHMM bucket or your own bucket) from:

* Quick start wizard (see [Configure query monitoring](watsonxdata?topic=watsonxdata-quick_start#qs_montr){: external})
* {{site.data.keyword.lakehouse_short}} console page (see [Query monitoring](watsonxdata?topic=watsonxdata-qhmm){: external})

You can retrieve the history files to analyze, debug, or monitor the queries. From the Query workspace see, [Retrieving query information from QHMM data](watsonxdata?topic=watsonxdata-ret_qhmm).

## Procedure
{: #prc_qhmm}

1. Log in to the {{site.data.keyword.lakehouse_short}} console.
2. From the navigation menu, select **Configurations**.
3. Click **Query monitoring**. The **Query monitoring** page opens.
4. You can view the QHMM configuration details. The following details are available:
    * Status of QHMM - Enabled or disabled.
    * Bucket that is configured to store QHMM data.
    * The subpath in the bucket where QHMM data is available.
5. To edit the configuration details, click **Edit** and make the required changes. You can enable or disable query monitoring, update sub-path and change the bucket.
6. Click **Save** after making the changes.
