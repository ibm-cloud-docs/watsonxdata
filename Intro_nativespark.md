---

copyright:
  years: 2017, 2024
lastupdated: "2024-11-06"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Introduction to Native Spark engine
{: #intro_nativespark}

Native Spark engine is a compute engine in {{site.data.keyword.lakehouse_full}}. You can use Native Spark engine to submit applications that involve complex analytical operations.

In {{site.data.keyword.lakehouse_short}}, Native Spark engine is used to achieve the following use cases:

- Ingest large volumes of data into {{site.data.keyword.lakehouse_short}} tables.
- Handle complex analytical workload.
- Table maintenance operation to enhance {{site.data.keyword.lakehouse_short}} performance of the table
- Develop, run, and debug applications written in Python, R, and Scala.

You can also register an external Spark engine from the **Add engine** window of the {{site.data.keyword.lakehouse_short}} UI. {{site.data.keyword.iae_full}} on Cloud is the external Spark engine here. To provision an external Spark engine on Cloud, see [Provisioning Analytics Engine]({{site.data.keyword.ref-lh-provisioning-serverless-link}}). For more information about registering the engine, see [Registering an engine]({{site.data.keyword.ref-reg_engine-link}}).
{: note}
