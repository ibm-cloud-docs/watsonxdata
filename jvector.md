---

copyright:
  years: 2022, 2025
lastupdated: "2025-12-17"

keywords: lakehouse, jvector, watsonx.data

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

# JVector integration with Presto (Private preview)
{: #jvector}

Similarity Search by using JVector is available as a Private Preview feature in Presto.
This capability enables users to create vector indexes and run Approximate Nearest Neighbor (ANN) Top‑K similarity searches on embedding data that is stored in Iceberg tables.
{: shortdesc}

**Overview**
{: #jvector_intro}

JVector is a high-performance Java library designed for vector indexing and Approximate Nearest Neighbor (ANN) search. It enables fast similarity search on high-dimensional embeddings and is commonly used in AI and ML search, recommendation systems, and database engines like Presto and Trino.
It supports efficient index creation, serialization, loading, and top-K vector search using distance metrics such as cosine or Euclidean similarity.


**Workflow**
{: #jvector_workflow}

1. Create a table with an embedding or vector column. Store embeddings as ARRAY type (native vector type not yet supported).

2. Create a JVector index on the vector column. Index files are stored in S3 for persistence and scalability.

3. Run ANN Top‑K queries. Retrieve the nearest neighbors efficiently by using the created index.

This feature is controlled by the flag: `iceberg.similarity-search-enabled` (default: false).
To enable the feature, add this property to the `iceberg.catalog.properties` file and set its value to `true`.

This capability is intended for early experimentation and feedback only and is not recommended for production use.
{: important}

**Key features**
{: #jvector_features}

* **Vector indexing in S3**: Users can create JVector-based vector indexes on embedding columns and store index files in object storage.

* **Top‑K similarity search**: Users can perform efficient nearest neighbor searches by using the created vector indexes.

* [**Jupyter Notebook tutorial**](https://github.com/IBM/watsonx-data/tree/main/Tutorials/presto-jvector-integration){: external}: Availability of a sample notebook for hands-on experience with index creation and ANN search workflows.

**Limitations**
{: #jvector_limitations}

* **Vector data type support**: Presto engines and Iceberg catalogs do not currently support vector data types natively. Embeddings are stored as ARRAY.

* **Index creation performance**:

  * Index creation time increases with dataset size.
  * Large datasets require manual partitioning because automatic splitting is not available.
  * Performance improvements and parallelization are needed for high-dimensional data.

* **Metadata management**: No robust layer for tracking index files, versioning, and associated table metadata.

* **Search scalability**: ANN search currently operates on a single index.

* **No Support for updates or deletes**: Indexes are static. Any data changes require a full index rebuild.

* **Memory considerations**: Index loading is memory-intensive. Ensure sufficient heap size based on vector dimension and index size.

* **No automatic failover**: Corrupted or missing index files require manual cleanup and recreation.

* **Data ingestion delay**: Ingestion is slow for large datasets due to the lack of an optimized pipeline. Smaller datasets are recommended for testing.
