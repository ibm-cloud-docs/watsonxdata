---

copyright:
  years: 2022, 2025
lastupdated: "2026-03-26"

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

# JVector integration with Spark (Private preview)
{: #jvector-spk}


The similarity search using JVector capability in Spark enables you to create vector indexes and perform Approximate Nearest Neighbor (ANN) Top‑K similarity searches on embedding data stored in Iceberg tables.


Note:
Similarity Search is controlled by the feature flag iceberg.similarity-search-enabled, which is set to false by default.
To enable the feature, add the property to the iceberg.catalog.properties file and set it to true.

## End-to-End Workflow
{: #jvector-wrflw}

A typical usage flow includes the following:

* Creating a table that contains an embedding (vector) column.
* Creating a JVector index on the vector column.
* Running ANN Top‑K queries to retrieve nearest neighbours.

**Key features**
{: #jvector_features-spk}

* **Vector indexing in S3**: Users can create JVector-based vector indexes on embedding columns and store index files in object storage.

* **Top‑K similarity search**: Users can perform efficient nearest neighbor searches by using the created vector indexes.

* [**Jupyter Notebook tutorial**](){: external}: Availability of a sample notebook for hands-on experience with index creation and ANN search workflows.

**Limitations**
{: #jvector_limitations_spk}

* **Vector data type support**: Spark engines and Iceberg catalogs do not currently support vector data types natively. Embeddings are stored as ARRAY.

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
