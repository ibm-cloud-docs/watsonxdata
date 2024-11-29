---

copyright:
  years: 2022, 2024
lastupdated: "2024-11-29"

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

# Milvus
{: #whatismilvus}

Milvus is a vector database that stores, indexes, and manages embedding vectors used for similarity search and retrieval augmented generation. It is developed to empower embedding similarity search and AI applications. Milvus makes unstructured data search more accessible and consistent across various environments.

watsonx.data uses version **2.4.0** of Milvus.

## What can you do with Milvus
{: #whatismilvus2}

With Milvus, you can perform various tasks that are related to managing and searching vector data, which is crucial for many artificial intelligence (AI) and machine learning (ML) applications. Here are some of the key things that you can do with Milvus:

### Vector similarity search
{: #whatismilvus2_1}

You can search for vectors similar to a query vector from millions of vectors in seconds. Vector similarity search in Milvus is a core feature that allows users to find vectors closest to a given query vector based on a specific metric of similarity. This capability is essential in many applications, such as recommendation systems, image and audio retrieval, natural language processing, and more.

### Hybrid search
{: #whatismilvus2_2}

Conducting a hybrid search in Milvus allows you to combine vector similarity search with traditional relational database-style filtering based on scalar fields. This feature is particularly useful when you need to refine your search results further by filtering on attributes like categories, timestamps, or any other metadata associated with your vectors. Hybrid search leverages both the vector embeddings and the scalar fields to provide more precise and relevant search results.

### Creating indexes
{: #whatismilvus2_3}

Indexing in Milvus involves organizing the data in a way that enables efficient query processing, especially for high-dimensional vector data. Milvus supports several types of indexes, each designed for specific scenarios or data characteristics.

### Recommendation Systems
{: #whatismilvus2_4}

You can use Milvus to power recommendation systems by finding items similar to your customer’s preferences or previous interactions.

For more information about Milvus, see:

- [Adding Milvus service]({{site.data.keyword.ref-adding-milvus-service-link}})
- [Connecting to Milvus service]({{site.data.keyword.ref-conn-to-milvus-link}})
- [Working with Milvus]({{site.data.keyword.ref-working_with_milvus-link}})
- [Pause and resume Milvus service]({{site.data.keyword.ref-pause_resume_milvus-link}})
- [Configuring IBM® watsonx.data Milvus in IBM watsonx.ai](watsonxdata?topic=watsonxdata-wxd_wxai_milvus_conn)
- [Birdwatcher debugging tool](watsonxdata?topic=watsonxdata-bd_dbgtool)
- [Connecting watsonx Assistant to watsonx.data Milvus for custom search](watsonxdata?topic=watsonxdata-wxd_wxa_connection)

You cannot upgrade from the private-preview version to the GA version of Milvus. You must delete the private preview and add the GA version.
{: important}
