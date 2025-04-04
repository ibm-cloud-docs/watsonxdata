---

copyright:
  years: 2022, 2025
lastupdated: "2025-03-24"

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

# Configuring {{site.data.keyword.lakehouse_full}} Milvus in IBM watsonx.ai
{: #wxd_wxai_milvus_conn}

If you are using IBM watsonx.ai, you can integrate Milvus vector database in {{site.data.keyword.lakehouse_short}} through the Milvus connector in platform connections.

## IBM watsonx.ai Prompt Lab
{: #wxai_pl}

IBM watsonx.ai Prompt Lab offers an interface for experimenting with various foundation models through engineered prompts. By incorporating retrieval-augmented generation (RAG) techniques, you can enhance model accuracy and relevance by adding grounding documents that contain context-specific information. These grounding documents, supported in formats like DOCX, PDF, PPTX, and TXT, are first converted into text embeddings by using pre-trained embedding models. Then, these embeddings are indexed by using Milvus vector database for efficient searching during prompt processing, ensuring more reliable and up-to-date responses.

For more information about Prompt Lab, see [Prompt Lab](https://dataplatform.cloud.ibm.com/docs/content/wsj/analyze-data/fm-prompt-lab.html?context=wx&audience=wdp).

To integrate the Milvus vector database in {{site.data.keyword.lakehouse_short}} through the Milvus connector in platform connections, you must:

- **Create a Milvus Service in {{site.data.keyword.lakehouse_short}}**: Set up Milvus in the {{site.data.keyword.lakehouse_short}} environment. For more information, see [Adding a Milvus service](/docs/watsonxdata?topic=watsonxdata-adding-milvus-service).
- **Create the Milvus Connection in platform connection**: Establish a connection to the Milvus service through the platform connection settings in watsonx.ai. For more information, [Milvus connection](https://dataplatform.cloud.ibm.com/docs/content/wsj/manage-data/conn-milvus.html?context=wx&audience=wdp).

To have a Milvus index as the grounding data in Prompt Lab, select or create a Milvus index from the Milvus connection. For more information, see [Creating a vector index](https://dataplatform.cloud.ibm.com/docs/content/wsj/analyze-data/fm-prompt-data-index-create.html?context=wx&audience=wdp).

## IBM watsonx.ai notebook
{: #wxai_nb}

If you want to run an IBM watsonx.ai notebook to complete the integration with Milvus database in {{site.data.keyword.lakehouse_short}}, you can use the Milvus connector and avoid entering the credentials directly into the notebook. For a sample notebook to implement a RAG use case with {{site.data.keyword.lakehouse_short}} Milvus and Milvus connector, see [sample notebook](https://github.com/IBM/watsonx-data/blob/main/Tutorials/watsonxdata-RAG-tutorial.ipynb).

For more information, see:

- [Connecting to Milvus service](/docs/watsonxdata?topic=watsonxdata-conn-to-milvus)
- [Creating and managing notebooks](https://dataplatform.cloud.ibm.com/docs/content/wsj/analyze-data/creating-notebooks.html?context=wx&audience=wdp)
