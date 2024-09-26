---

copyright:
  years: 2022, 2024
lastupdated: "2024-09-24"

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

You can view the metrics using Sysdig. Do the following steps to set up and monitor metrics (as a non-operation user).

1. Go to the [IBM Access Hub](https://ibm-support.saviyntcloud.com/ECMv6/request/applicationRequest).
1. search and select **HDM-Lakehouse-IBM-Cloud-Dev-IAM-2592207**. The user details appear under the **Existing Accounts** section of the pop-up window.
1. Click **Modify**. The **Modify Access** window opens.
1. Click **Add** to add the group and click **Done**.
1. Click **Review & Submit**. You can review the details in the page.
1. Enter a business justification, select the checkbox to confirm the reviewed details, and click **Submit**.
1. After getting the Sysdig access, log in to your {{site.data.keyword.cloud_notm}} account and access the {{site.data.keyword.cloud_notm}} console.
1. In the left pane, go to **Observability** > **Monitoring** > **Instances**. You can see a list of entries for different regions.
1. Choose the region where your Milvus service is located and click **Open dashboard** to open the Sysdig dashboard. On the Sysdig dashboard, you can either browse through or search for *milvus* to view a list of the Milvus specific metrics.

For information about the metrics that are exposed by Milvus, see [Metrics exposed by Milvus](watsonxdata?topic=watsonxdata-milvus_exp_metrics_list).
