---

copyright:
  years: 2022, 2024
lastupdated: "2024-07-03"

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
{:attention: .attention}

# Pause and resume Milvus service
{: #pause_resume_milvus}

You can pause and resume a Milvus service from the **Infrastructure manager**.
{: shortdesc}

- To pause a Milvus service:
   1. From the navigation menu, select **Infrastructure manager**.
   1. From the topology view, hover over the Milvus service tile that you want to pause. A pause icon appears.
   1. Click the pause icon. \
      Alternatively, from the list view, go to the overflow menu of the Milvus service and select **Pause**. \
   A confirmation box appears with the message: `Any in-flight queries running on this service will be terminated`.
   1. Click **Pause** to confirm.
- To resume a Milvus service:
   1. From the navigation menu, select **Infrastructure manager**.
   1. From the topology view, hover over the Milvus service tile that you want to resume. A resume icon appears.
   1. Click the resume icon. \
      Alternatively, from the list view, go to the overflow menu of the Milvus service and select **Resume**.

Milvus compute is not billed during the pause time.
{: note}
