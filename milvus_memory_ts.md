---

copyright:
  years: 2017, 2024
lastupdated: "2024-08-21"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Why is Milvus unresponsive?
{: #mlvs_mmry_ts}
{: troubleshoot}

The query nodes crash and any further queries that are made are not completed.
{: tsSymptoms}


Milvus might become unresponsive if the consumed memory of the loaded collections exceeds the capacity of the cluster.
{: tsCauses}

If there are multiple collections that are loaded, release some of them to free up memory. In PyMilvus, you can do it using:
{: tsResolve}

```bash
   client.release_collection("collection_name")
```
{: codeblock}

The released collections must be loaded again if you want to search them.
{: note}

If a single collection doesn't fit in the memory, you cannot query the collection to retrieve data. To recover the collection:

- Increase the query node memory by doing the following:

    - Upgrade the size.
    - Increase the query node replicas.

- Reduce the collection size by doing the following:

    - Delete rows.
    - Extract the required data from the collection, drop the collection, and then reset the size. Alternatively, continue to use the upgraded size without modifying the collection.
