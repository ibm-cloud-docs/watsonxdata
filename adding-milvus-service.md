---

copyright:
  years: 2022, 2024
lastupdated: "2025-02-25"

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
    |  | **Custom**: Recommended for upto **3 billion vectors**, 64 index parameters, and 1024 segment. The actual number of vectors and dimensions supported depends on the index type and the maximum supported vCPU configuration. \n - IVF_SQ8: Up to 3 billion vectors. \n - IVF_FLAT: Up to 1.3 billion vectors. \n - HNSW: Up to 1 billion vectors. |
    | Add storage bucket | Associate an external storage for the **Small**, **Medium**, or **Large** sizes. For **Starter** size, you can also select an IBM-managed storage. To associate an external storage, you must have the storage configured.|
    | Path | For external storages, specify the path where you want to store vectorized data files.|
    {: caption="Adding Milvus service" caption-side="bottom"}

    Milvus now allows scaling up between predefined T-shirt sizes (small, medium, large) or custom sizes.
    Scaling down Milvus may impact performance when reducing from a higher capacity. If collections no longer fit into memory after scaling down, service might be impacted. In case of a service impact, the only solution is to either drop the collection or scale back up. Even if the service do not crash, the collections that were previously loaded but now exceed available memory may encounter issues.
    {: important}

    Scaling operation introduces a 5 to 10 minutes service delay. Ongoing operations may be disrupted during scaling transitions.
    {: note}

    For more information about adding external storages, see [Adding a storage-catalog pair]({{site.data.keyword.ref-reg_bucket-link}}){: external}.

    If the schema of the collection changes (an increase in the number of fields in a collection or increase in the size of the `varchar` field beyond 256 characters, or if multiple vector fields are added into the collection), the number of records might decrease.
    {: important}

    Milvus service can connect to a storage without a catalog. You can perform the actions on Milvus even after disabling the storage.
    {: note}

    You must provide the endpoint for storages used by Milvus with the region for region-specific storages like S3 and without trailing slashes. For example: `https://s3.<REGION>.amazonaws.com`.
    {: important}

5. Click **Create**.

## Related API
{: #addmilvus_api}

For information on related API, see
* [Get list of milvus services](https://cloud.ibm.com/apidocs/watsonxdata#list-milvus-services)
* [Create milvus service](https://cloud.ibm.com/apidocs/watsonxdata#create-milvus-service)
