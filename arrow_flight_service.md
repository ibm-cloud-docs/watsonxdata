---

copyright:
  years: 2022, 2024
lastupdated: "2024-12-10"

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

# Arrow Flight service overview
{: #arrow_database}

You can connect to the data source through the Arrow Flight service that is deployed on IBM Cloud. You need to enter the details that are related to the API key and Flight service URL. This feature is applicable for both Presto (Java) and Presto (C++) engines.
{: shortdesc}

## Prerequisites
{: #prereq_database}

* The Arrow Flight connector supports only the IBM Arrow Flight service on an IBM Cloud.
* The Arrow Flight service should be running for data sources to work with.

## Features and capabilities
{: #features_database}

* The data sources that are supported through Arrow Flight service have better performance as compared to JDBC data sources.
* Basic query pushdown is available for queries across the tables from the same data source and across the tables from different flight data sources.
* The Arrow Flight service data sources support only `SELECT` and `DESCRIBE` queries.

## Procedure
{: #procedure_database}

1. Log in to {{site.data.keyword.lakehouse_full}} instance.
2. From the navigation menu, select **Infrastructure manager**.
3. To define and connect a data source, click **Add component**.
4. In the **Add component** window, select a data source from the **Data source** section.
5. The following data sources are supported for Arrow Flight service:
* [Apache Derby](watsonxdata?topic=watsonxdata-derby_database){: external}
* [Greenplum](watsonxdata?topic=watsonxdata-greenplum_database){: external}
* [MariaDB](watsonxdata?topic=watsonxdata-mariadb_database){: external}
* [Salesforce](watsonxdata?topic=watsonxdata-salesforce_database){: external}
