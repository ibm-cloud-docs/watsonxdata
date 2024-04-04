---

copyright:
  years: 2022, 2024
lastupdated: "2024-04-03"

keywords: lakehouse, hudi, connector, watsonx.data

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

# Integrating Presto with Apache Hudi using a Hudi connector
{: #hudi-conn}

You can integrate Presto with Apache Hudi by using the Hudi connector. You can query Hudi tables that are synced to Hive metastore (HMS) using Presto's SQL interface. This combination offers the benefits of fast and interactive analytics on large-scale, high-velocity data stored in Hudi. Hudi connector uses the metastore to track partition locations. It uses underlying Hudi file system and input formats to list data files.
{: shortdesc}

## Configuring a catalog in Presto
{: #conf-cat}

Create a hudi.properties file inside /opt/presto/etc/catalog directory in the presto container.

```bash
# hudi.properties
connector.name=hudi

# HMS thrift URI
hive.metastore.uri=thrift://<hostname>:<port>

# properties to enable connection to object-storage bucket
hive.s3.ssl.enabled=true
hive.s3.path-style-access=true
hive.s3.endpoint=<Bucket API Endpoint>
hive.s3.aws-access-key=<INSERT YOUR ACCESS KEY>
hive.s3.aws-secret-key=<INSERT YOUR SECRET KEY>

# properties to enable TLS connection to HMS
hive.metastore.thrift.client.tls.enabled=true
hive.metastore.authentication.type=PLAIN
hive.metastore.thrift.client.tls.truststore.path=<Truststore Path>
hive.metastore.thrift.client.tls.truststore.password=<Truststore Password>
hive.metastore.thrift.client.tls.keystore.path=<Keystore Path>
hive.metastore.thrift.client.tls.keystore.password=<Keystore Password>
```

## Limitations
{: #limitations}

1. Connector does not support DDL or DML SQL statements. Presto can query data using the Hudi connector, but cannot directly perform write operations.
2. Data modifications must be done through Hudi-specific tools and workflows.
