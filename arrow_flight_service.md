---

copyright:
  years: 2022, 2024
lastupdated: "2024-08-02"

keywords: lakehouse, database, watsonx.data

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

# Arrow Flight service overview
{: #arrow_database}

You can connect to the databases through the Arrow Flight service that is deployed on IBM Cloud. You need to enter the details that are related to API key and Flight service URL. This feature is applicable for both Presto (Java) and Presto (C++) engines.
{: shortdesc}

## Prerequisites
{: #prereq_database}

1. The Arrow Flight connector supports only the IBM Arrow Flight service on an IBM Cloud VM.
2. The Arrow Flight service should be running for databases to work with.

## Features and capabilities
{: #features_database}

1. The databases that are supported through Arrow Flight service have better performance as compared to JDBC databases.
2. Basic query pushdown is available for queries across the tables from the same database and across the tables from different flight databases.
3. The Arrow Flight service databases support only `SELECT` and `DESCRIBE` queries.

## Procedure
{: #procedure_database}

1. Log in to {{site.data.keyword.lakehouse_full}} instance.
2. From the navigation menu, select **Infrastructure manager**.
3. To define and connect a database, click **Add component** and select **Add database**.
4. In the **Add database** window, select a database from the **Database type** drop-down list.
5. The following databases are supported for Arrow Flight service:
* [Apache Derby](watsonxdata?topic=watsonxdata-derby_database){: external}
* [Greenplum](watsonxdata?topic=watsonxdata-greenplum_database){: external}
* [MariaDB](watsonxdata?topic=watsonxdata-mariadb_database){: external}
* [Salesforce](watsonxdata?topic=watsonxdata-salesforce_database){: external}
