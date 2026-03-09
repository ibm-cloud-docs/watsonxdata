---

copyright:
  years: 2022, 2025
lastupdated: "2026-02-11"

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

This configuration is available only with the Gen AI experience.
{: note}

Configure the foundation model that powers retrieval-based tasks in {{site.data.keyword.lakehouse_short}}.

## About this task
{: #abtist}

The Retrieval Service in {{site.data.keyword.lakehouse_short}} enables administrators to configure which foundation model powers retrieval-based tasks such as text-to-SQL, question answering, and RAG. At the instance level, you can choose between granite (default), llama and gpt models, based on licensing and workload requirements

## Configuring the retrieval service model
{: #congretm}

1. Log in to {{site.data.keyword.lakehouse_short}} console.
1. From the navigation menu, select **Configurations** and click **Retrieval service model** tile.
1. Under **Retrival service** section, choose one of the following available AI models:
   - **granite-3-8b-instruct**
   - **llama-3-3-70b-instruct**
   - **gpt-oss-120b**

    <br>To use **gpt-oss-120b** with the Retrieval Service, you must first deploy the model in **toronto region**. For detailed instructions, see [Deploying foundation models on demand (fast path)](https://dataplatform.cloud.ibm.com/docs/content/wsj/analyze-data/deploy-on-demand-resource-hub.html?context=wx&audience=wdp).
    {: note}

1. A confirmation dialog appears, click **Select**.

## Configuring the Text to SQL model
{: #contts}

1. In the **Text to SQL** section, select the AI model to use for Text to SQL conversion:
   - **granite-3-8b-instruct**
   - **llama-3-3-70b-instruct**
1. A confirmation dialog appears, click **Select**.
