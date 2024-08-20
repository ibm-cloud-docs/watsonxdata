---

copyright:
  years: 2022, 2024
lastupdated: "2024-08-13"

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

# Adding Milvus service
{: #adding-milvus-service}

Milvus is a vector database that stores, indexes, and manages massive embedding vectors that are developed by deep neural networks and other machine learning (ML) models. It is developed to empower embedding similarity search and AI applications. Milvus makes unstructured data search more accessible and consistent across various environments.
{: shortdesc}

The version **2.4.0** of `pymilvus` is recommended for Milvus 2.4.x. Uninstall the earlier version and install the latest version of `pymilvus`.
{: note}

Complete the following steps to add Milvus as a service in {{site.data.keyword.lakehouse_full}}.

1. Log in to the {{site.data.keyword.lakehouse_short}} console.
2. From the navigation menu, select **Infrastructure Manager**.
3. To define and connect to a service, click **Add component**, select **Milvus**, and click **Next**.
4. In the **Add component - Milvus** window, provide the following details.

    | Field | Description |
    | -------- | -------- |
    | Display name | Enter the Milvus service name to be displayed on the screen.|
    | Size | Select the suitable size.|
    |  | **Starter**: Recommended for **1 million vectors**, 64 index parameters, 1024 segment size, and 384 dimensions. |
    |  | **Small**: Recommended for **10 million vectors**, 64 index parameters, 1024 segment size, and 384 dimensions. |
    |  | **Medium**: Recommended for **50 million vectors**, 64 index parameters, 1024 segment size, and 384 dimensions. |
    |  | **Large**: Recommended for **100 million vectors**, 64 index parameters, 1024 segment size, and 384 dimensions. |
    | Add storage bucket | Associate an external bucket for the **Small**, **Medium**, or **Large** sizes. For **Starter** size, you can also select an IBM-managed bucket. To associate an external bucket, you must have the bucket configured.|
    | Path | For external buckets, specify the path where you want to store vectorized data files.|
    {: caption="Table 1. Adding Milvus service" caption-side="bottom"}

    For more information about adding external buckets, see [Adding a storage-catalog pair]({{site.data.keyword.ref-reg_bucket-link}}){: external}.

    If the schema of the collection changes (an increase in the number of fields in a collection or increase in the size of the `varchar` field beyond 256 characters, or if multiple vector fields are added into the collection), the number of records might decrease.
    {: important}

    Milvus service can connect to a storage without a catalog. You can perform the actions on Milvus even after disabling the storage.
    {: note}

    You must provide the endpoint for buckets used by Milvus with the region for region-specific buckets like S3 and without trailing slashes. For example: `https://s3.<REGION>.amazonaws.com`.
    {: important}

5. Click **Create**.
