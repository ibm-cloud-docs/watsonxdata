---

copyright:
  years: 2022, 2026
lastupdated: "2026-03-22"

keywords: lakehouse, remote data, confluent, {{site.data.keyword.lakehouse_short}}

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

# Integrating Confluent Tableflow in {{site.data.keyword.lakehouse_short}}
{: #data_stream_confluent1}

You can integrate Confluent Tableflow with {{site.data.keyword.lakehouse_full}} to enable zero-copy querying of remote data. Confluent offers a data platform that acts as a central nervous system for real-time data, enabling businesses to connect, store, and manage data across cloud and on-premise environments.

Confluent Tableflow automatically converts Apache Kafka topics into ready-to-query Apache Iceberg tables, enabling zero-copy, real-time analytics through data federation. It eliminates complex data pipelines by materializing data in user-owned or managed storage with automated maintenance.

## How it works
{: #data_stream_confluent1_1}

1. Create a Kafka cluster in Confluent Cloud.
2. Create topics to stream your data.
3. Enable Tableflow for topics to convert them into Iceberg tables.
4. Query the remote tables using {{site.data.keyword.lakehouse_short}} Spark or Presto engines without copying data.

## Storage options
{: #data_stream_confluent1_2}

- **Confluent managed storage**: Confluent automatically provisions and manages AWS S3 storage. No additional setup required.
- **Customer integration**: Use your own cloud storage (AWS S3, Azure Blob, or Google Cloud Storage) with full control over data location and access.

## Key features
{: #data_stream_confluent1_3}

- Zero-copy data access
- Real-time data availability in Iceberg format
- Automatic schema evolution
- Query federation through {{site.data.keyword.lakehouse_short}}
- Integration with {{site.data.keyword.lakehouse_short}} compute engines

## Important limitations
{: #data_stream_confluent1_4}

- Tableflow tables are read-only from external compute engines.
- Write operations (`INSERT`, `CREATE TABLE`, `UPDATE`, `DELETE`) are not supported when querying through {{site.data.keyword.lakehouse_short}}.
- Data can only be modified by publishing messages to the source Kafka topic

For more information, see [Confluent TableFlow documentation](https://docs.confluent.io/cloud/current/topics/tableflow/overview.html).

## Next steps
{: #data_stream_confluent1_5}

- [Querying Confluent TableFlow using Spark engine](/docs/watsonxdata?topic=watsonxdata-data_stream_confluent2spark)
- [Querying Confluent TableFlow using Presto engine](/docs/watsonxdata?topic=watsonxdata-data_stream_confluent3presto)
