---

copyright:
  years: 2022, 2025
lastupdated: "2025-10-27"

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

# Spark engine
{: #spk_ovrviw}

The {{site.data.keyword.lakehouse_short}} platform includes a built-in native Spark engine that allows you to perform big data analytics seamlessly. Additionally, {{site.data.keyword.lakehouse_short}} supports external Spark engines, enabling you to leverage Spark clusters outside of the {{site.data.keyword.lakehouse_short}} environment. You can use {{site.data.keyword.lakehouse_short}} Spark engine to achieve the following use cases:

1. Ingesting large volumes of data into {{site.data.keyword.lakehouse_short}} tables. You can also cleanse and transform data before ingestion.
2. Table maintenance operation to enhance {{site.data.keyword.lakehouse_short}} performance of the table
3. Complex analytics workload which are difficult to represent as queries.

For more information about provisioning the engine, see [Provisioning a Spark engine](/docs/watsonxdata?topic=watsonxdata-spl_engine).

{{site.data.keyword.lakehouse_full}} allows you to integratrate with the following types of Spark:

**Native Spark engine**
Native Spark engine is a compute engine that is available within {{site.data.keyword.lakehouse_short}} instance. With native Spark engine, you can fully manage Spark Engine configuration, manage access to Spark Engines and run applications by using watsonx.data UI and REST API endpoints.

For more information, see [Provisioning a native Spark engine](/docs/watsonxdata?topic=watsonxdata-spl_engine){: external}.

**Gluten accelerated Spark engine**
Performance optimized data processing engine capable of processing Spark applications. It uses Gluten, which relies on Velox (C++) generic database acceleration library that optimize the queries. This is an effective solution to speed up and simplify your process if you work with very huge data set. For more information, see Gluten accelerated Spark engine.

For more information, see [Provisioning Gluten accelerated Spark engine](/docs/watsonxdata?topic=watsonxdata-prov_cpp){: external}.

**External Spark engine**
External Spark engines are engines that exist in a different cluster from where {{site.data.keyword.lakehouse_short}} is provisioned. You can deploy them in the following environments:
* Spark instance on Cloud
* Spark on EMR

The option to register external Spark engines in watsonx.data is deprecated and will be removed in version 2.3. watsonx.data already includes built-in Spark engines that you can provision and use directly, including the Gluten-accelerated Spark engine and the native watsonx.data Spark engine.
{: important}
