---

copyright:
  years: 2022, 2024
lastupdated: "2024-04-03"

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

See [Create a Collection](https://milvus.io/docs/v2.3.x/create_collection.md) for creating collection in Milvus.

## Inserting data in Milvus
{: #working_with_milvus-02}

Milvus supports default values for scalar fields except a primary key field. You can keep some fields empty during data inserts.

For more information, see [Insert data to Milvus](https://milvus.io/docs/v2.3.x/insert_data.md#Insert-data-to-Milvus).

It is recommended to insert your data in batches due to following reasons:

   - The number of vectors that can be ingested in a single GRPC API call is limited by the maximum message size allowed by Kafka.

   - The maximum number of rows that can be inserted at a time depends on the total size of the data you are trying to ingest. The exact number decreases with the increase in the dimensions of the vector and the presence of non-vector fields in the row.

It is recommended to use to use the bulk insert API  for inserting the data-sets greater than 500,000 vectors. Ingest performance of the bulk insert API is better than that of the batch insert API.
{: note}


## Creating indexes in Milvus
{: #working_with_milvus-03}

Create an index before you conduct the Approximate Nearest Neighbor (ANN) search in Milvus.

IBM officially supports the following indexes:

Indexes that are not listed in this list might work, but are not validated by IBM.
{: note}

   - HNSW
   - SCANN
   - FLAT
   - IVF_FLAT
   - IVF_PQ

GPU based indexes do not work in {{site.data.keyword.lakehouse_short}}.

You can create the index by specifying the vector field name and index parameters. For more information, see [Build an Index on Vectors](https://milvus.io/docs/v2.3.x/build_index.md).

## Conducting a vector similarity search in Milvus
{: #working_with_milvus-04}

In Milvus, you can conduct a vector similarity search after you prepare the parameters for your search scenario.

For more information, see [Conduct a Vector Similarity Search](https://milvus.io/docs/v2.3.x/search.md).

## Conducting a hybrid search in Milvus
{: #working_with_milvus-05}

In Milvus, you can conduct a hybrid search based on vector similarity and scalar filtering. For more information, see [Conduct a Hybrid Search](https://milvus.io/docs/v2.3.x/hybridsearch.md).

## Conducting a query based on scalar filtering in Milvus
{: #working_with_milvus-06}

In Milvus, you can conduct a query based on scalar filtering. For more information, see [Conduct a Query](https://milvus.io/docs/v2.3.x/query.md).

When running a search query with scalar filtering on a large data set, it is important to adjust the limit parameter to manage query results effectively. Use the following approach to set the limit parameter:
```bash
hello_milvus.query(expr=query_condition, output_fields=["random", "embeddings"], limit=100,offset=0)
```
{: codeblock}
{: note}

The sum of the values of limit and offset parameters must be in the range of [1, 16384].

## Deleting entities from Milvus by using primary key
{: #working_with_milvus-07}

In Milvus, you can delete the entities by using primary key. You need to prepare the Boolean expression that filters the entities to delete.

For more information, see [Delete Entities](https://milvus.io/docs/v2.3.x/delete_data.md).

## Dropping a collection from Milvus
{: #working_with_milvus-08}

Dropping a collection from Milvus is irreversible. You cannot recover the deleted data.
{: attention }

Run the following Python command to drop a collection.

```bash
from pymilvus import utility
utility.drop_collection(<collection name>)
```
{: codeblock}
