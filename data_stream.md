---

copyright:
  years: 2022, 2026
lastupdated: "2026-03-16"

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

# Integrating data streaming platforms
{: #data_stream}

{{site.data.keyword.lakehouse_full}} supports integration with modern data streaming platforms that enable real-time data ingestion and analytics. These platforms convert streaming data into query-ready table formats like Apache Iceberg or Delta Lake, eliminating the need for complex ETL pipelines.

## Supported platforms
{: #data_stream1}

{{site.data.keyword.lakehouse_full}} integrates with the following data streaming platforms:
- Confluent Tableflow
- Databricks

## Key capabilities
{: #data_stream2}

When you integrate data streaming platforms with {{site.data.keyword.lakehouse_short}}, you can:
- Query real-time streaming data using Spark and Presto engines
- Access Iceberg and Delta Lake tables without data movement
- Eliminate complex ETL processes with zero-ETL analytics
- Leverage existing streaming infrastructure with {{site.data.keyword.lakehouse_short}} compute engines

## Integration architecture
{: #data_stream3}

Data streaming platforms materialize streaming data into table formats in cloud storage (AWS S3, Azure Blob, Google Cloud Storage). {{site.data.keyword.lakehouse_short}} engines connect to these tables through REST catalog endpoints, enabling direct querying without data duplication.

## Choosing an engine
{: #data_stream4}

- **Spark engine**: Supports both managed and provider-integrated storage, full Iceberg feature support
- **Presto engine**: Supports provider-integrated storage (AWS S3, Azure, GCS) with some limitations on managed storage

### Next steps
{: #data_stream5}

- [Integrating Confluent Tableflow](/docs/watsonxdata?topic=watsonxdata-data_stream_confluent1)
