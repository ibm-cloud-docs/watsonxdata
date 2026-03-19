---

copyright:
  years: 2022, 2026
lastupdated: "2026-03-19"

keywords: lakehouse, data streaming, {{site.data.keyword.lakehouse_short}}

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

# Remote lakehouse access
{: #data_stream}

Remote lakehouse platforms enable continuous data ingestion and processing, allowing organizations to capture, store, and analyze data as it flows through their systems. These platforms act as a central nervous system for real-time data, connecting various data sources and making sharing data immediately available for analytics.

{{site.data.keyword.lakehouse_full}} integrates with leading third-party lakehouse platforms to provide seamless access to remote data without copying or moving it. These integrations enable you to query remote data using familiar SQL interfaces and powerful compute engines.


## How remote lakehouse integrations work
{: #data_stream1}

Third-party lakehouse platforms automatically convert streaming data into query-ready table formats such as Apache Iceberg. This zero-copy approach, often called "data federation" or "query federation," eliminates the need for traditional data pipelines by:


1. Capturing sharing data from various sources (applications, IoT devices, databases, etc.)
2. Materializing data into open table formats in cloud storage (AWS S3, Azure Blob Storage, Google Cloud Storage)
3. Maintaining tables automatically with schema evolution, compaction, and optimization
4. Exposing data through REST catalog endpoints for external query engines

{{site.data.keyword.lakehouse_short}} compute engines connect directly to these remote tables, enabling zero-copy analytics without data duplication or movement.



## Key capabilities
{: #data_stream2}

When you integrate third-party lakehouse platforms with {{site.data.keyword.lakehouse_short}}, you can:

- Query remote data in real-time: Access the latest data as it arrives, with minimal latency
- Eliminate data copying and ETL complexity: Remove the need for custom data pipelines and transformation jobs
- Use familiar SQL interfaces: Query remote lakehouse data using standard SQL through Spark or Presto engines
- Leverage open table formats: Work with industry-standard formats like Apache Iceberg and Delta Lake
- Maintain data governance: Apply watsonx.data's security and governance policies to remote
- Scale independently: Separate storage and compute for flexible scaling and cost optimization
- Preserve data lineage: Track data from source to analytics with built-in metadata management

## Integration architecture
{: #data_stream3}

Remote lakehouse platforms materialize remote data into table formats in cloud storage (AWS S3, Azure Blob, Google Cloud Storage). {{site.data.keyword.lakehouse_short}} engines connect to these tables through REST catalog endpoints, enabling direct querying without data duplication.

## Storage options
{: #data_stream4}

Third-party lakehouse platforms typically offer two storage models:

- Platform-managed storage: The lakehouse platform automatically provisions and manages cloud storage, simplifying setup and maintenance.
- Customer-managed storage: You provide your own cloud storage (AWS S3, Azure Blob, or Google Cloud Storage), maintaining full control over data location, access policies, and lifecycle management.

Both options are supported by {{site.data.keyword.lakehouse_short}}, though specific engine capabilities may vary.

## Choosing an engine
{: #data_stream5}

- **Spark engine**: Supports both managed and customer-managed storage, full Iceberg feature support.
- **Presto engine**: Supports customer-managed storage (AWS S3, Azure, GCS) with some limitations on managed storage.

### Next steps
{: #data_stream6}

- [Integrating Confluent Tableflow](/docs/watsonxdata?topic=watsonxdata-data_stream_confluent1)
