---

copyright:
  years: 2022, 2024
lastupdated: "2024-10-28"

keywords: lakehouse, milvus, watsonx.data

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

# Milvus metrics
{: #milvus_exp_metrics}

Milvus exposes various metrics, which will provide in-depth insights into various system parameters from the observability and serviceability perspectives. You get real-time update on how the Milvus components are performing and utilized.

To view the metrics, you must create an IBM Cloud Monitoring instance and enable it for platform metrics. For more information, see [Getting started with IBM Cloud Monitoring](https://cloud.ibm.com/docs/monitoring?topic=monitoring-getting-started#getting-started).

1. Log in to your {{site.data.keyword.cloud_notm}} account and access the {{site.data.keyword.cloud_notm}} console.
1. In the left pane, go to **Observability** > **Monitoring** > **Instances**. You can see a list of entries for different regions.
1. Choose the region where your Milvus service is located and click **Open dashboard** to open the Sysdig dashboard. On the Sysdig dashboard, you can either browse through or search for *milvus* to view a list of the Milvus specific metrics.

For information about the metrics that are exposed by Milvus, see [Metrics exposed by Milvus](watsonxdata?topic=watsonxdata-milvus_exp_metrics_list).
