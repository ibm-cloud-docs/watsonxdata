---

copyright:
  years: 2022, 2025
lastupdated: "2025-12-02"

keywords: lakehouse, watsonx.data, query optimizer, install

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

# Configure AI model for Retrieval Service
{: #retsrvc}

The Retrieval Service in {{site.data.keyword.lakehouse_short}} enables administrators to configure which foundation model powers retrieval-based tasks such as text-to-SQL, question answering, and RAG. At the instance level, you can choose between granite (default), llama and gpt models, based on licensing and workload requirements.

## Procedure
{: #install_retsrvc}

1. Log in to {{site.data.keyword.lakehouse_short}} console.
1. From the navigation menu, select **Configurations** and click **Retrieval service model** tile.
1. Under **Retrival service** section, choose one of the following avialble AI models:
   - **granite-3-8b-instruct**
   - **llama-3-3-70b-instruct**
   - **gpt-oss-120b**

    <br>To use **gpt-oss-120b** with the Retrieval Service, you must first deploy the model in **toronto region**. For detailed instructions, see [Deploying foundation models on demand (fast path)](https://dataplatform.cloud.ibm.com/docs/content/wsj/analyze-data/deploy-on-demand-resource-hub.html?context=wx&audience=wdp).
    {: note}

1. A confirmation dialog appears, click **Select**.
1. Under **Text to SQL**, choose on of the following avialble AI models:
   - **granite-3-8b-instruct**
   - **llama-3-3-70b-instruct**
1. A confirmation dialog appears, click **Select**.
