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

# Configuring Query monitoring
{: #qhmm}

Query History Monitoring and Management (QHMM) is a service that stores and manages diagnostic data, such as  heap dumps, thread dumps, query history and query event-related information of the Presto engine (Presto) in the default Minio bucket, wxd-system. You can retrieve the history files to analyze, debug or monitor the queries. You can also store the data in your own bucket.
{: shortdesc}

You can enable or disable the QHMM service for your {{site.data.keyword.lakehouse_short}} instance. If you enable the QHMM service, you must specify the storage to be used for storing the query data.
{{site.data.keyword.lakehouse_short}} allows using the default storage, `wxd-system` to store the QHMM data or register your own storage (BYOB). To use BYOB, register your bucket in watsonx.data and configure it to use as QHMM storage. You can do that either from Quick start or from {{site.data.keyword.lakehouse_short}} console page. For more information, see [Retrieving query information from QHMM data]({{site.data.keyword.ref-ret_qhmm-link}}).

You can choose the QHMM storage (default QHMM bucket or your own bucket) from:

* Quick start wizard (see [Configure query monitoring]({{site.data.keyword.ref-quick_start-link}}))
* {{site.data.keyword.lakehouse_short}} console page (see [Query monitoring]({{site.data.keyword.ref-qhmm-link}}))

You can retrieve the history files to analyze, debug, or monitor the queries. From the Query workspace see, [Retrieving query information from QHMM data]({{site.data.keyword.ref-ret_qhmm-link}}).

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
6. You can edit the data pruning feature for QHMM. You can do the following:
    * Enable the file pruning functionality in QHMM to manage the storage capacity. You can configure the maximum size and threshold percentage for the QHMM storage bucket. When the threshold is met during file upload or when a cleanup scheduler runs (default every 24 hours), older data is deleted.
    * Pruning threshod: Threshold at which QHMM triggers pruning or issues a warning when the capacity reaches the threshold percentage (default: 80%).
    * Pruning frequency: Frequency in hours at which pruning occurs (default: 24 hours).
    * Maximum usage: Maximum capacity of the bucket in MB (default: 10240 MB).
    * Pruned records retention period: Record expiry time in days for deleting records from COS (default: 30 days).

6. Click **Save** after making the changes.
