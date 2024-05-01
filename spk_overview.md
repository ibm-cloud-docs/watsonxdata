---

copyright:
  years: 2022, 2024
lastupdated: "2024-04-30"

keywords: watsonx.data, data ingestion, source file

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

# About Spark engine
{: #spk_ovrviw}

The {{site.data.keyword.lakehouse_short}} platform includes a built-in native Spark engine that allows you to perform big data analytics seamlessly. Additionally, {{site.data.keyword.lakehouse_short}} supports external Spark engines, enabling you to leverage Spark clusters outside of the {{site.data.keyword.lakehouse_short}} environment. You can use {{site.data.keyword.lakehouse_short}} Spark engine to achieve the following use cases:

1. Ingesting large volumes of data into {{site.data.keyword.lakehouse_short}} tables. You can also cleanse and transform data before ingestion.
2. Table maintenance operation to enhance {{site.data.keyword.lakehouse_short}} performance of the table
3. Complex analytics workload which are difficult to represent as queries.

{{site.data.keyword.lakehouse_full}} allows you to integratrate with the following types of Spark:

**Native Spark engine**
Native Spark engine is a compute engine that is available within {{site.data.keyword.lakehouse_short}} instance. With native Spark engine, you can fully manage Spark Engine configuration, manage access to Spark Engines and run applications by using watsonx.data UI and REST API endpoints.

For more information, see Working with native Spark engine section.

**External Spark engine**
External Spark engines are engines that exist in a different cluster from where {{site.data.keyword.lakehouse_short}} is provisioned. You can deploy them in the following environments:
* Spark instance on Cloud
* Spark on EMR

For more information, see Working with external Spark engine section.
