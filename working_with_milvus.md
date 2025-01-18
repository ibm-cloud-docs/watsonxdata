---

copyright:
  years: 2022, 2024
lastupdated: "2025-01-16"

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

# Working with Milvus
{: #working_with_milvus}

## Creating a collection in Milvus
{: #working_with_milvus-01}

In Milvus, collections are used to store and manage entities. A **collection** in Milvus is equivalent to a table in a relational database management system (RDBMS).

See [Create a Collection](https://milvus.io/docs/manage-collections.md#Create-Collection) for creating collection in Milvus.

## Inserting data in Milvus
{: #working_with_milvus-02}

Milvus supports default values for scalar fields except a primary key field. You can keep some fields empty during data inserts.

For more information, see [Insert entries](https://milvus.io/docs/insert-update-delete.md#Insert-Upsert--Delete).


It is recommended to insert your data in batches due to the following reasons:

- The number of vectors that can be ingested in a single GRPC API call is limited by the maximum message size that is allowed by Kafka. In IBM Cloud, the maximum limit of message size is limited to 1 MB.

- The maximum number of rows that can be inserted at a time depends on the total size of the data you are trying to ingest. The exact number decreases with the increase in the dimensions of the vector and the presence of non-vector fields in the row.

Use the bulk insert API for inserting the data sets larger than 500,000 vectors. The bulk insert API performs better than the batch insert API when ingesting larger data sets. If you are using batch insert API, manually flush the collection after every 500,000 rows. For more information, see [Bulk Insert API](https://milvus.io/api-reference/pymilvus/v2.4.x/ORM/utility/do_bulk_insert.md).
{: note}


## Creating indexes in Milvus
{: #working_with_milvus-03}

Create an index before you conduct the Approximate Nearest Neighbor (ANN) search in Milvus.

IBM officially supports the following indexes:

Indexes that are not listed in this list might work, but are not validated by IBM.
{: note}

When the number of rows in a segment is less than 1024, Milvus will not create any indexes for that segment. Instead, it will default to using `brute-force` search for query operations. Once the row count in the segment exceeds this threshold, Milvus will automatically begin building the indexes.
{: note}

- HNSW
- SCANN
- FLAT
- IVF_FLAT
- IVF_PQ

You can create the index by specifying the vector field name and index parameters. For more information, see [Index Vector Fields](https://milvus.io/docs/index-vector-fields.md?tab=floating).

## Conducting a vector similarity search in Milvus
{: #working_with_milvus-04}

In Milvus, you can conduct a vector similarity search after you prepare the parameters for your search scenario.

- For more information about single-vector and multi-vector search, see [Vector similarity search](https://milvus.io/docs/single-vector-search.md).
- For more information about hybrid (multi-vector) search, see [Hybrid search](https://milvus.io/docs/multi-vector-search.md).

## Conducting a query based on scalar filtering in Milvus
{: #working_with_milvus-06}

In Milvus, you can conduct a query based on scalar filtering. For more information, see [Get & scalar query](https://milvus.io/docs/get-and-scalar-query.md).

You can do the following search types:

- Range search: To find vectors within a specific distance range from the query vector. For more information, see [Range search](https://milvus.io/docs/single-vector-search.md#Range-search).
- Grouping search: To get results based on a specific field to ensure diversity in the results. For more information, see [Grouping search](https://milvus.io/docs/single-vector-search.md#Grouping-search).

When running a search query with scalar filtering on a large data set, it is important to adjust the limit parameter to manage query results effectively. Use the following approach to set the `limit` parameter:
```bash
hello_milvus.query(expr=query_condition, output_fields=["random", "embeddings"], limit=100,offset=0)
```
{: codeblock}
{: note}

The sum of the values of `limit` and `offset` parameters must be in the range of [1, 16384].

## Deleting entities from Milvus by using primary key
{: #working_with_milvus-07}

In Milvus, you can delete the entities by using primary key. Prepare the Boolean expression that filters the entities to delete.

For more information, see [Delete Entities](https://milvus.io/docs/insert-update-delete.md#Delete-entities).

## Dropping a collection from Milvus
{: #working_with_milvus-08}

Dropping a collection from Milvus is irreversible. You cannot recover the deleted data.
{: attention }

Add the following to your `.ipynb` or Python script to drop a collection..

```bash
from pymilvus import utility
utility.drop_collection(<collection name>)
```
{: codeblock}

## Best practices
{: #bestpractice_milvus}

Following are some best practices:

- If there are long Varchar fields (greater than 256 characters), keep non-vector fields outside of Milvus. You can keep them in a COS bucket or storage bucket and perform a referential search.
- Make sure that the PyMilvus version is 2.4.0 or later. Milvus 2.4.0 or later versions support sparse vector search, hybrid search (`sparse_dense`), and multi vector search.
- While loading collections by using batch insert, follow the pattern: Insert in a batch, release the memory, and then repeat the process.
- Don't ingest in parallel to all of the collections at once. Ingest sequentially and flush between ingests.
- Each collection's maximum size should be corresponding to the maximum number of vectors supported in a T-shirt size.
- If you have multiple collections or partitions loaded, ensure that the sum of vectors in all loaded entities does not exceed the limit of the T-shirt size. You can still store more vectors than the T-shirt size limit as long as the number of vectors that are loaded is within the limit.

During Milvus upgrade, there can be a slight delay in response for about 20 seconds. On-going searches and upsert queries might fail. You can retry the queries immediately.
{: note}
