---

copyright:
  years: 2022, 2024
lastupdated: "2024-12-05"

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

Metadata Service is a component of {{site.data.keyword.lakehouse_short}} that acts as the centralized metadata repository and plays a crucial role in managing and storing metadata for tables, databases, partitions, and other objects. MDS acts as the centre for metadata management that allows different frameworks in a distributed data ecosystem to access the underlying data by using shared schema definitions consistently.
{: shortdesc}

MDS offers two interfaces for interaction:

## REST API interface
{: #mdsov_rest}

REST API interface includes selected APIs from Iceberg REST Catalog Open API Spec and Open Source Unity Catalog API Spec.

## Apache Thrift interface (HMS APIs)
{: #mdsov_thrift}

Engines such as Native Spark and Presto in WXD are implicitly connected to the MDS through the Apache Thrift interface, which implements the standard HMS functions. Other HMS Client applications such as the Iceberg Hive Catalog client can also be configured to connect to the HMS interface of MDS. These HMS APIs enable interaction with the MDS to:

- Retrieve table or database schemas.
- Get partition information for optimized query execution.
- Add, alter, or drop databases, tables, and partitions.

Apart from the HMS interface, MDS also implements selected APIs from the Iceberg REST Catalog and Unity Catalog Open API spec. You can leverage these APIs from standard REST Clients to Spark and Presto for invoking the API. Use of REST Client has the benefit of directly interacting with the metastore without an engine. These REST interfaces offers interoperability benefits with other external systems as well.

For information about retrieving credentials, see [Retrieving Metadata Service (MDS) credentials](watsonxdata?topic=watsonxdata-hms).

For information about using AWS EMR for Spark, see [Using AWS EMR for Spark use case](watsonxdata?topic=watsonxdata-spark-emr).

For information about working with Apache Hudi catalogm, [see Working with Apache Hudi catalog](watsonxdata?topic=watsonxdata-hudi_ext_sp).
