---

copyright:
  years: 2022, 2024
lastupdated: "2024-07-03"

keywords: lakehouse, hms, watsonx.data, hive, metastore

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

# HMS Overview
{: #hms_overview}

## Hive Metastore
{: #hms_intro}

Hive Metastore (HMS) is a service that stores metadata related to Presto (Java) and other services in a backend Relational Database Management System (RDBMS) or Hadoop Distributed File System (HDFS).
{: shortdesc}

When you create a new table, information related to the schema such as column names, data types etc is stored in the metastore relational database. A metastore enables the user to see the data files in the HDFS object storage as if they are stored in tables with HMS.

Metastore acts as a bridge between the schema of the table and the data files stored in object storages. HMS holds the definitions, schema, and other metadata for each table and maps the data files and directories to the table representation which is viewed by the user. Therefore, HMS is used as a storage location for the schema and tables. HMS is a metastore server that connects to the object storage to store data and keeps its related metadata on PostgreSQL.

Any database with a JDBC driver can be used as a metastore. Presto (Java) makes requests through thrift protocol to HMS. The Presto (Java) instance reads and writes data to HMS. HMS supports 5 backend databases as follows. In {{site.data.keyword.lakehouse_full}}, PostgreSQL database is used.
* Derby
* MySQL
* MS SQL Server
* Oracle
* PostgreSQL

Currently HMS in {{site.data.keyword.lakehouse_short}} supports Iceberg table format.

Following three modes of deployment are supported for HMS. In {{site.data.keyword.lakehouse_short}} the remote mode is used.
* Embedded Metastore - Derby with singe session.
* Local Metastore - MySQl with multiple session accessible locally.
* Remote Metastore - metastore runs on its own separate JVM and accessible via thrift network APIs.
