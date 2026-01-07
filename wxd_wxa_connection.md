---

copyright:
  years: 2022, 2025
lastupdated: "2025-12-18"

keywords: lakehouse, **Query Optimizer**, {{site.data.keyword.lakehouse_short}}

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

# Connecting watsonx Assistant to {{site.data.keyword.lakehouse_short}} Milvus for custom search
{: #wxd_wxa_connection}

Connecting watsonx Assistant to {{site.data.keyword.lakehouse_short}} Milvus allows you to use the power of Milvus for vector similarity search and indexing in your data. With this connection, you can integrate Milvus into your watsonx workflow and take advantage of its high performance and scalability.

To connect watsonx Assistant to Milvus in {{site.data.keyword.lakehouse_short}}, do the following steps:

1. Create a Milvus service instance in {{site.data.keyword.lakehouse_short}}. For more information, see [Adding Milvus service](/docs/watsonxdata?topic=watsonxdata-adding-milvus-service).
1. Connect to the Milvus service. For more information about connecting to a Milvus service, see [Connecting to Milvus service](/docs/watsonxdata?topic=watsonxdata-conn-to-milvus).
1. Insert data into the Milvus instance.
   - For information about inserting vectorized data into Milvus, see [Insert, Upsert & Delete](https://milvus.io/docs/insert-update-delete.md).
   - If you want to insert non-vectorized data, for example a PDF file, use embedding models to vectorize it. You can use watsonx.ai that has vectorizing embeddings. For more information, see [Milvus connection](https://dataplatform.cloud.ibm.com/docs/content/wsj/manage-data/conn-milvus.html?context=wx&audience=wdp) in watsonx.ai. Use `ibmlhapikey_<username>` as username and your [API key]({{site.data.keyword.ref-con-presto-serv-link}}#get-ibmapi-key) as password for the Milvus connection.

   For information about {{site.data.keyword.lakehouse_short}} Milvus configuration in watsonx.ai, see [Configuring IBM® watsonx.data Milvus in IBM watsonx.ai](/docs/watsonxdata?topic=watsonxdata-wxd_wxai_milvus_conn).
   {: note}

1. Set up your watsonx Assistant instance. For more information, see [Getting started with watsonx Assistant](https://cloud.ibm.com/docs/watson-assistant?topic=watson-assistant-getting-started).
1. Connect to Milvus service from watsonx Assistant by using one of the following options:
   * Access Milvus service directly from watsonx Assistant. For more information, see [Milvus search integration setup](https://cloud.ibm.com/docs/watson-assistant?topic=watson-assistant-search-milvus-add#setup-milvus).
   * Set up a custom service in watsonx Assistant. For more information, see [Custom service integration setup](https://cloud.ibm.com/docs/watson-assistant?topic=watson-assistant-search-customsearch-add#setup-custom-service-server). You can use the Custom 	 Service option for advanced capabilities, such as:

      * Flexibility to use any Milvus that is supported.
      * Multi-vector hybrid search.
      * Reranking.
      * Hybrid search with GroupBy.

        Milvus does not support aggregation in Hybrid GroupBy search.
        {: note}
