---

copyright:
  years: 2022, 2025
lastupdated: "2025-03-24"

keywords: lakehouse, metadata, service, mds, watsonx.data

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

# Metadata Service (MDS)
{: #mdsov}

Metadata Service is a component of {{site.data.keyword.lakehouse_short}} that acts as the centralized metadata repository and plays a crucial role in managing and storing metadata for tables, databases, partitions, and other objects. MDS acts as the center for metadata management that allows different frameworks in a distributed data ecosystem to access the underlying data by using shared schema definitions consistently.
{: shortdesc}

For existing {{site.data.keyword.lakehouse_short}} instances: For external engine integrations like Db2, Netezza, and Analytics Engine, you must change the HMS thrift endpoint to MDS thrift endpoint.
{: important}

To configure the pool size for the maximum number of connections in a connection pool in MDS, contact the SRE or the support team.
{: note}

MDS offers two interfaces for interaction:

## Apache Thrift interface (HMS APIs)
{: #mdsov_thrift}

Engines such as Native Spark and Presto in {{site.data.keyword.lakehouse_short}} are implicitly connected to MDS through the Apache Thrift interface, which implements the standard HMS functions. Other HMS Client applications such as the Iceberg Hive Catalog client can also be configured to connect to the HMS interface of MDS. These HMS APIs enable interaction with the MDS to:

- Retrieve table or database schemas.
- Get partition information for optimized query execution.
- Add, alter, or drop databases, tables, and partitions.


## REST API interface
{: #mdsov_rest}

REST API interface includes selected APIs from Iceberg REST Catalog Open API Spec and Open Source Unity Catalog API Spec. MDS also implements selected APIs from the Iceberg REST Catalog and Unity Catalog Open API spec. You can leverage these APIs from standard REST Clients to Spark and Presto. Use of REST Client has the benefit of directly interacting with the metastore without an engine. These REST interfaces offer interoperability benefits with other external systems as well.

For information about Unity and Iceberg Catalog REST API, see [Unity Catalog REST API and Iceberg Catalog REST API](/docs/watsonxdata?topic=watsonxdata-unity_iceberg_api).
