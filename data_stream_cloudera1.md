---

copyright:
  years: 2022, 2026
lastupdated: "2026-05-05"

keywords: lakehouse, remote data, cloudera, {{site.data.keyword.lakehouse_short}}

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

# Integrating Cloudera in {{site.data.keyword.lakehouse_short}}
{: #data_stream_cloudera1}

You can integrate Cloudera with {{site.data.keyword.lakehouse_full}} to enable zero-copy querying of remote data. Cloudera provides an enterprise data platform that enables organizations to manage, process, and analyze data across hybrid and multi-cloud environments.

By integrating Cloudera with {{site.data.keyword.lakehouse_short}}, you can query Hive tables stored in Cloudera HDFS without copying data, enabling seamless data federation across your data landscape.

## How it works
{: #data_stream_cloudera1_1}

1. Create Hive tables in Cloudera using the Hue editor.
2. Configure HDFS storage component in {{site.data.keyword.lakehouse_short}}.
3. Associate the catalog with your Presto engine.
4. Query the remote tables using {{site.data.keyword.lakehouse_short}} Presto engine without copying data.

## Architecture overview
{: #data_stream_cloudera1_2}

The integration works through the following components:

1. **Cloudera HDFS** - Distributed file system storing Hive table data
2. **Hive Metastore** - Centralized metadata repository for table definitions
3. **{{site.data.keyword.lakehouse_short}} Presto engine** - Query engine that executes queries
4. **HDFS Storage Component** - Bridge between {{site.data.keyword.lakehouse_short}} and Cloudera

## Supported table and storage formats
{: #data_stream_cloudera1_4}

- **Hive tables** - Query Hive tables stored in various formats (Parquet, ORC, Avro, Text)
- **Storage formats** - Parquet, ORC, Avro, Text files

## Key features
{: #data_stream_cloudera1_5}

- Zero-copy data access
- Support for both Kerberos and non-Kerberos authentication
- Query federation through {{site.data.keyword.lakehouse_short}}
- Integration with {{site.data.keyword.lakehouse_short}} Presto engine
- Direct access to Hive Metastore

## Important limitations
{: #data_stream_cloudera1_6}

- Only Presto engine is supported for querying Cloudera tables
- Tables are read-only from {{site.data.keyword.lakehouse_short}}
- `UPDATE` and `DELETE` operations are not supported when querying Hive tables through {{site.data.keyword.lakehouse_short}}
- Data modifications must be performed directly in Cloudera

## Security considerations
{: #data_stream_cloudera1_7}

**Authentication:**

- **Non-Kerberos:** Suitable for development and testing environments with basic HDFS user authentication
- **Kerberos:** Recommended for production environments with enterprise-grade security

**Data access:**

- All queries execute with the permissions of the authenticated user or principal
- HDFS enforces file-level security policies
- Storage credentials must have appropriate read permissions on HDFS locations

**Network security:**

- Ensure network connectivity between {{site.data.keyword.lakehouse_short}} and Cloudera cluster
- Configure firewall rules to allow traffic on required ports (HDFS NameNode, Hive Metastore)
- For Kerberos, ensure connectivity to KDC (Key Distribution Center)

## Next steps
{: #data_stream_cloudera1_8}

- [Setting up Cloudera integration with Presto engine](/docs/watsonxdata?topic=watsonxdata-data_stream_cloudera_presto_setup)
- [Querying Cloudera tables using Presto engine](/docs/watsonxdata?topic=watsonxdata-data_stream_cloudera_presto_query)

## Related information
{: #data_stream_cloudera1_9}

- [Cloudera Data Platform documentation](https://docs.cloudera.com/)
- [Apache Hive documentation](https://hive.apache.org/)
- [Apache HDFS documentation](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsUserGuide.html)
