---

copyright:
  years: 2022, 2026
lastupdated: "2026-04-30"

keywords: lakehouse, remote data, external data, data federation, {{site.data.keyword.lakehouse_short}}

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

# Accessing data in external data platforms
{: #data_stream}

{{site.data.keyword.lakehouse_full}} enables you to query data from multiple external data platforms without copying or moving the data. This capability provides seamless access to data across your data landscape while maintaining data in its original location.
{: shortdesc}

## Overview
{: #data_stream_overview}

With {{site.data.keyword.lakehouse_short}}, you can access and query data from external platforms through direct connections. This approach eliminates the need to replicate data, providing:

- **Real-time access** - Query the most current data without synchronization delays
- **Cost efficiency** - Eliminate storage duplication and data transfer costs
- **Simplified architecture** - Reduce data pipeline complexity and maintenance overhead
- **Unified governance** - Apply consistent security and access policies across data sources

This integration method is commonly known as zero-copy data federation, where queries are executed directly on remote data through secure connections.

## Supported external data platforms
{: #data_stream_platforms}

{{site.data.keyword.lakehouse_short}} supports querying data from the following external platforms:

### Cloudera
{: #data_stream_cloudera}

Access Hive tables stored in Cloudera HDFS for enterprise data warehousing and Hadoop ecosystem integration.

**Learn more:** [Integrating Cloudera in {{site.data.keyword.lakehouse_short}}](/docs/watsonxdata?topic=watsonxdata-data_stream_cloudera1)

### Databricks Unity Catalog
{: #data_stream_databricks}

Access Delta Lake and Iceberg tables stored in Databricks Unity Catalog for multi-cloud data analytics and unified data governance.

**Learn more:** [Integrating Databricks Unity Catalog in {{site.data.keyword.lakehouse_short}}](/docs/watsonxdata?topic=watsonxdata-data_stream_databricks1)

### Snowflake Open Catalog
{: #data_stream_snowflake}

Access Apache Iceberg tables managed by Snowflake Open Catalog for cloud-native data analytics and cross-platform data access.

**Learn more:** [Integrating Snowflake Open Catalog in {{site.data.keyword.lakehouse_short}}](/docs/watsonxdata?topic=watsonxdata-data_stream_snowflake1)

### Confluent Tableflow
{: #data_stream_confluent}

Access streaming data tables managed by Confluent Tableflow for real-time analytics and event-driven architectures.

**Learn more:** [Querying Confluent Tableflow using Spark engine](/docs/watsonxdata?topic=watsonxdata-data_stream_confluent2spark)

### Salesforce
{: #data_stream_salesforce}

Connect to Salesforce data through Arrow Flight service for CRM analytics and customer data integration.

**Learn more:** [Salesforce](/docs/watsonxdata?topic=watsonxdata-salesforce_database)

## How it works
{: #data_stream_architecture}

Accessing external data in {{site.data.keyword.lakehouse_short}} works through the following components:

1. **External data platform** - The remote system where data resides
2. **Metadata layer** - Catalog or metastore that provides table definitions and schema information
3. **{{site.data.keyword.lakehouse_short}} engines** - Presto or Spark engines that execute queries
4. **Storage layer** - External storage systems where data files are stored
5. **Authentication layer** - Security mechanisms for secure access

## Query engines
{: #data_stream_engines}

{{site.data.keyword.lakehouse_short}} supports querying external data through two query engines:

- **Presto engine** - Optimized for interactive analytics with SQL-based querying
- **Spark engine** - Optimized for batch processing and complex transformations with PySpark and Scala support

For details on which platforms support which engines, see the platform-specific integration guides.

## Getting started
{: #data_stream_getting_started}

To access data from external platforms:

1. **Identify data platforms** - Determine which external platforms you need to access
2. **Review prerequisites** - Ensure you meet the requirements for each platform
3. **Gather credentials** - Obtain necessary authentication credentials and connection details
4. **Configure connections** - Set up storage components and catalogs in {{site.data.keyword.lakehouse_short}}
5. **Associate engines** - Connect catalogs to appropriate query engines
6. **Test queries** - Validate connectivity and query functionality

For detailed setup instructions, see the integration guide for your specific platform.

## Related information
{: #data_stream_related}

**Integration guides:**
- [Integrating Cloudera in {{site.data.keyword.lakehouse_short}}](/docs/watsonxdata?topic=watsonxdata-data_stream_cloudera1)
- [Integrating Databricks Unity Catalog in {{site.data.keyword.lakehouse_short}}](/docs/watsonxdata?topic=watsonxdata-data_stream_databricks1)
- [Integrating Snowflake Open Catalog in {{site.data.keyword.lakehouse_short}}](/docs/watsonxdata?topic=watsonxdata-data_stream_snowflake1)
- [Querying Confluent Tableflow using Spark engine](/docs/watsonxdata?topic=watsonxdata-data_stream_confluent2spark)
- [Salesforce](/docs/watsonxdata?topic=watsonxdata-salesforce_database)
