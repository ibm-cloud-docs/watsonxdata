---

copyright:
  years: 2022, 2025
lastupdated: "2025-08-26"

keywords: lakehouse, watsonx.data, presto

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

# Presto (Java)
{: #presto_overview}

Presto (Java) is a distributed SQL query engine, with the capability to query vast data sets located in different data sources, thus solving data problems at scale.
{: shortdesc}

Presto (Java) provides the ANSI SQL interface, which can be used for all data analytics and {{site.data.keyword.lakehouse_full}} use cases. With this feature, you do not need to manage multiple query languages and interfaces to different databases and storage. Presto (Java) is designed for storage abstraction, which allows connections to any data source through its connectors.

For more information about provisioning the engine, see [Provisioning a Presto (Java) engine](/docs/watsonxdata?topic=watsonxdata-prov_engine).

## Presto (Java) server types
{: #lh-presto_servertypes}

A Presto (Java) installation includes three server types - Coordinator, Worker, and Resource manager. Following is a brief explanation of the server types. For more information about the server types, see [Presto (Java) concepts](https://prestodb.io/docs/current/overview/concepts.html) in Presto (Java) documentation.

- Coordinator - A coordinator is a server type in a Presto (Java) installation, which is responsible for parsing statements, planning queries, and managing Presto (Java) worker nodes. It is the brain of a Presto (Java) installation and is also the node to which a client connects to submit statements for execution. It is also responsible for fetching results from the workers and returning the results to the client.

- Worker - A worker is a server type in a Presto (Java) installation, which is responsible for running tasks and processing data. Worker nodes fetch data from connectors and exchange intermediate data with each other.

- Resource manager - The resource manager is a server type in Presto (Java), which aggregates data from all coordinator and workers and creates a global view of the Presto (Java) cluster.

For more information on supported connectors, see [Adding a database-catalog pair](/docs/watsonxdata?topic=watsonxdata-reg_database).

## Presto (Java) SQL Language
{: #lh-presto_lang}

For more information about SQL language used in Presto (Java), see [SQL Language](https://prestodb.io/docs/current/language.html){: external} in Presto (Java) documentation.

### Data types
{: #lh-presto_datatypes}

By default, Presto (Java) supports the following data types. More types can be provided by plug-ins:

- Boolean
- Integer
- Floating-Point
- Fixed-Precision
- String
- Date and Time
- Structural
- Network Address
- UUID
- HyperLogLog
- KHyperLogLog
- Quantile Digest
- T-Digest

For more information about the data types, see [Data types](https://prestodb.io/docs/current/language/types.html){: external} in Presto (Java) documentation.

### Reserved keywords
{: #lh-presto_keywords}

Presto (Java) has a set of reserved keywords for SQL queries. These keywords must be quoted in double quotation marks to be used as an identifier.
For the list of reserved keywords, see [Reserved keywords](https://prestodb.io/docs/current/language/reserved.html){: external} in Presto (Java) documentation.

### SQL Syntax
{: #lh-presto_syntax}

For more information about SQL syntax used in Presto (Java), see [SQL statements](https://www.ibm.com/docs/en/watsonx/watsonxdata/2.1.x?topic=presto-sql-statements){: external}.
