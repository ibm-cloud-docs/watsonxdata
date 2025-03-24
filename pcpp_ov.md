---

copyright:
  years: 2017, 2025
lastupdated: "2025-03-24"

keywords: watsonx.data, spark, emr
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Presto (C++)
{: #pcpp_ov}

Presto (C++) is a version of Presto workers that are implemented in C++ instead of Java by using the Velox library.

Presto (C++) aims to enhance performance for data lakes without requiring a JVM on worker nodes. It supports several connectors, including Hive and Iceberg, and focuses on improved integration with data warehousing systems.

{{site.data.keyword.lakehouse_full}} uses version **0.286** of Presto (C++).

## Presto (C++) features
{: #pcpp_ftr}

* **Task management**: Presto C++ includes HTTP endpoints that allow users to monitor and manage tasks. This feature enhances operational oversight and makes it easier to track ongoing processes.
* **Remote function execution**: Enables executing functions on remote nodes, which enhance scalability and distributed processing capabilities, making data processing more efficient across a network of nodes.
* **Authentication**: Uses JSON Web Tokens (JWT) for secure internal communication between nodes, ensuring that data remains secure and tamper-proof during transmission.
* **Data caching**: Implements asynchronous data caching with prefetching capabilities. This optimizes data retrieval and processing speed by anticipating data needs and caching it in advance.
* **Performance Tuning**: Offers various session properties for performance tuning, including settings for spill thresholds and compression. This allows users to fine-tune performance parameters according to their specific needs, ensuring optimal performance of data processing tasks.

For more information about Presto (C++), see [Presto C++ features](https://prestodb.io/docs/current/presto_cpp/features.html).

For more information about provisioning a Presto (C++) engine, see [Provisioning a Presto (C++) engine](/docs/watsonxdata?topic=watsonxdata-pcpp_prov).

For more information about customizing properties, see:

* [Configuration properties for Presto (C++) - worker nodes](/docs/watsonxdata?topic=watsonxdata-api_custom_wkr_pcpp)
* [Configuration properties for Presto (C++) - coordinator nodes](/docs/watsonxdata?topic=watsonxdata-aapi_custom_pcpp_cood)
* [Catalog properties for Presto (C++)](/docs/watsonxdata?topic=watsonxdata-api_custom_pcpp_ctg)
* [Velox properties for Presto (C++)](/docs/watsonxdata?topic=watsonxdata-api_custom_pcpp_vlx)
