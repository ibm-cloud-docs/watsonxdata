---

copyright:
  years: 2022, 2024
lastupdated: "2024-09-19"

keywords: lakehouse, data source, watsonx.data

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

# Adding a data source-catalog pair
{: #reg_database}

You can register and use data source in {{site.data.keyword.lakehouse_full}}. A catalog defines the schemas and metadata for a data source.
{: shortdesc}

When you add your own object storage bucket or data source, or query the data in these data sources through the query engines of {{site.data.keyword.lakehouse_short}}, egress charges for pulling data out of these sources might apply depending on your service provider. If you are using managed services, consult your service provider's documentation or support for details about these charges.
{: important}

To reduce the latency issues, it is recommended to colocate your additional object storage buckets or data source in the region where {{site.data.keyword.lakehouse_short}} instance is provisioned.
{: important}


To add data source-catalog pair, complete the following steps.

1. Log in to the {{site.data.keyword.lakehouse_short}} instance.
2. From the navigation menu, select **Infrastructure manager**.
3. To add a data source, click **Add component**.
4. In the **Add component**, select a data source from the **Data source** section.
5. Based on the data source type selected, configure the data source details.
6. You can associate a catalog to the data source. This catalog can be associated with an engine. A catalog defines the schemas and metadata for a storage or data source. Depending on the storage type, Apache Iceberg, Apache Hive, Apache Hudi, and Delta Lake catalogs are supported.

    Two data sources with the same name cannot be added.
   {: note}

The following data sources are supported:
* [Amazon Redshift](watsonxdata?topic=watsonxdata-redshift_database)
* [Apache Druid](watsonxdata?topic=watsonxdata-druid_database)
* [Apache Kafka](watsonxdata?topic=watsonxdata-kafka_database)
* [Apache Pinot](watsonxdata?topic=watsonxdata-pinot_database)
* [BigQuery](watsonxdata?topic=watsonxdata-bigquery_database)
* [Cassandra](watsonxdata?topic=watsonxdata-cassandra_database)
* [ClickHouse](watsonxdata?topic=watsonxdata-clickhouse_database)
* [Elasticsearch](watsonxdata?topic=watsonxdata-elasticsearch_database)
* [IBM Data Virtualization Manager for z/OS](watsonxdata?topic=watsonxdata-dvm_database)
* [IBM Db2](watsonxdata?topic=watsonxdata-db2_database)
* [IBM NPSaaS](watsonxdata?topic=watsonxdata-netezza_database)
* [Informix](watsonxdata?topic=watsonxdata-informix_database)
* [MongoDB](watsonxdata?topic=watsonxdata-mongodb_database)
* [MySQL](watsonxdata?topic=watsonxdata-mysql_database)
* [Oracle](watsonxdata?topic=watsonxdata-oracle_database)
* [PostgreSQL](watsonxdata?topic=watsonxdata-postgresql_database)
* [Prometheus](watsonxdata?topic=watsonxdata-prometheus_database)
* [Redis](watsonxdata?topic=watsonxdata-redis_database)
* [SingleStore](watsonxdata?topic=watsonxdata-singlestore_database)
* [Snowflake](watsonxdata?topic=watsonxdata-snowflake_database)
* [SQL Server](watsonxdata?topic=watsonxdata-sqlserver_database)
* [Teradata](watsonxdata?topic=watsonxdata-teradata_database)
* [Custom data source](watsonxdata?topic=watsonxdata-custom_database)
* Arrow Flight Service:
* [Apache Derby](watsonxdata?topic=watsonxdata-derby_database)
* [Greenplum](watsonxdata?topic=watsonxdata-greenplum_database)
* [MariaDB](watsonxdata?topic=watsonxdata-mariadb_database)
* [Salesforce](watsonxdata?topic=watsonxdata-salesforce_database)


For more information on mixed-case feature flag behavior, supported SQL statements and supported data types matrices, see [Support content](https://www.ibm.com/support/pages/node/7157339){: external}.
