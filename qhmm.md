---

copyright:
  years: 2022, 2024
lastupdated: "2024-10-28"

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

Query History Monitoring and Management (QHMM) is a service that stores and manages diagnostic data, such as  heap dumps, thread dumps, query history and query event-related information of the Presto engine (Presto) in the storage associated with a Hive catalog. You can retrieve the history files to analyze, debug or monitor the queries. You can also store the data in your own bucket.
{: shortdesc}

You can enable or disable the QHMM service for your {{site.data.keyword.lakehouse_short}} instance. If you enable the QHMM service, you must specify the storage to be used for storing the query data.
You must create and associate a Hive catalog to store the QHMM data (register your own storage (BYOB)). To use BYOB, register your bucket (Hive storage) in watsonx.data and configure it to use as QHMM storage. You can do that either from Quick start or from {{site.data.keyword.lakehouse_short}} console page. For more information, see [Retrieving query information from QHMM data]({{site.data.keyword.ref-ret_qhmm-link}}).

QHMM supports only Hive storage.
{: note}

## Enabling QHMM feature
{: #enb_qhmm}

You can enable the QHMM feature in one of the following ways:

* Quick start wizard. See [Configure query monitoring](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-quick_start#qs_montr).
* [{{site.data.keyword.lakehouse_short}} console](#prc_qhmm) page.

You can retrieve the history files to analyze, debug, or monitor the queries. From the Query workspace see, [Retrieving query information from QHMM data]({{site.data.keyword.ref-ret_qhmm-link}}).


## Procedure
{: #prc_qhmm}

1. Log in to the {{site.data.keyword.lakehouse_short}} console.
2. From the navigation menu, select **Configurations**.
3. Click **Query monitoring**. The **Query monitoring** page opens.
4. If you enabled QHMM feature at the time of provisioning watsonx.data quick start, you can view the QHMM configuration details. The following details are available:
    * Status of QHMM - Enabled or disabled.
    * Bucket that is configured to store QHMM data.
    * The subpath in the bucket where QHMM data is available.

   To edit the configuration details, click **Edit** and make the required changes.You can enable or disable query monitoring, update sub-path and change the bucket.
   {: note}

5. If the QHMM feature is not enabled at the time of provisioning watsonx.data quick start, you can do that from the **Query monitoring** page.

    1. Create a storage - catlaog (Apache Hive) pair in watsonx.data. See [Adding a storage-catalog pair]({{site.data.keyword.ref-reg_bucket-link}}){: external}. QHMM supports only the Apache Hive catalog.

    2. Click **Edit**.

    3. Select the **Enable** check box. You can select the check box only if you have created a Hive catalog in watsonx.data.

    4. Select the Hive catalog from the **Storage**.

    5. You can also update the sub-path.

    6. You can edit the data pruning feature for QHMM. You can do the following:

        * Enable the file pruning functionality in QHMM to manage the storage capacity. You can configure the maximum size and threshold percentage for the QHMM storage bucket. When the threshold is met during file upload or when a cleanup scheduler runs (default every 24 hours), older data is deleted.

        * Pruning threshod: Threshold at which QHMM triggers pruning or issues a warning when the capacity reaches the threshold percentage (default: 80%).

        * Pruning frequency: Frequency in hours at which pruning occurs (default: 24 hours).

        * Maximum usage: Maximum capacity of the bucket in MB (default: 10240 MB).

        * Pruned records retention period: Record expiry time in days for deleting records from COS (default: 30 days).


    6. Click **Save** after making the changes.
