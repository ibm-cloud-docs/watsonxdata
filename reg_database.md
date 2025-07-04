---

copyright:
  years: 2022, 2025
lastupdated: "2025-06-23"

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

# Adding data source
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
4. In the **Add component** window, select a data source from the **Data source** section and provide the details to establish the connection.

    Two data sources with the same name cannot be added.
   {: note}

{{site.data.keyword.lakehouse_short}} supports the following data source options:
* [Amazon Redshift]({{site.data.keyword.ref-redshift_database-link}})
* [Apache Druid]({{site.data.keyword.ref-druid_database-link}})
* [Apache Kafka]({{site.data.keyword.ref-kafka_database-link}})
* [Apache Phoenix](/docs/watsonxdata?topic=watsonxdata-phoenix_database)
* [Apache Pinot]({{site.data.keyword.ref-pinot_database-link}})
* [BigQuery]({{site.data.keyword.ref-bigquery_database-link}})
* [Cassandra]({{site.data.keyword.ref-cassandra_database-link}})
* [ClickHouse]({{site.data.keyword.ref-clickhouse_database-link}})
* [Elasticsearch]({{site.data.keyword.ref-elasticsearch_database-link}})
* [HANA](/docs/watsonxdata?topic=watsonxdata-saphana_database)
* [IBM Data Virtualization Manager for z/OS]({{site.data.keyword.ref-dvm_database-link}})
* [IBM Db2]({{site.data.keyword.ref-db2_database-link}})
* [IBM NPSaaS]({{site.data.keyword.ref-netezza_database-link}})
* [Informix]({{site.data.keyword.ref-informix_database-link}})
* [MongoDB]({{site.data.keyword.ref-mongodb_database-link}})
* [MySQL]({{site.data.keyword.ref-mysql_database-link}})
* [Oracle]({{site.data.keyword.ref-oracle_database-link}})
* [PostgreSQL]({{site.data.keyword.ref-postgresql_database-link}})
* [Prometheus]({{site.data.keyword.ref-prometheus_database-link}})
* [Redis]({{site.data.keyword.ref-redis_database-link}})
* [SingleStore]({{site.data.keyword.ref-singlestore_database-link}})
* [Snowflake]({{site.data.keyword.ref-snowflake_database-link}})
* [SQL Server]({{site.data.keyword.ref-sqlserver_database-link}})
* [Teradata]({{site.data.keyword.ref-teradata_database-link}})
* [Custom data source]({{site.data.keyword.ref-custom_database-link}})
* Arrow Flight Service:
* [Apache Derby]({{site.data.keyword.ref-derby_database-link}})
* [Greenplum]({{site.data.keyword.ref-greenplum_database-link}})
* [MariaDB]({{site.data.keyword.ref-mariadb_database-link}})
* [Salesforce]({{site.data.keyword.ref-salesforce_database-link}})


For more information on mixed-case feature flag behavior, supported SQL statements and supported data types matrices, see [Support content](https://www.ibm.com/support/pages/node/7157339){: external}.

## Related API
{: #datasource_api}

For information on related API, see
* [Get databases](https://cloud.ibm.com/apidocs/watsonxdata#list-database-registrations)
* [Add/create database](https://cloud.ibm.com/apidocs/watsonxdata#create-database-registration)
* [Get database](https://cloud.ibm.com/apidocs/watsonxdata#get-database)
