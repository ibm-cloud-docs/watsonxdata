---

copyright:
  years: 2017, 2025
lastupdated: "2026-02-11"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.lakehouse_short}} Spark engine
{: #intro_nativespark}

Native Spark engine is a compute engine in {{site.data.keyword.lakehouse_full}}. You can use Native Spark engine to submit applications that involve complex analytical operations.

In {{site.data.keyword.lakehouse_short}}, native Spark engine is used to achieve the following use cases:

- Ingest large volumes of data into {{site.data.keyword.lakehouse_short}} tables.
- Handle complex analytical workload.
- Table maintenance operation to enhance {{site.data.keyword.lakehouse_short}} performance of the table
- Develop, run, and debug applications written in Python, R, and Scala.

For more information about using Spark engine, see [Working with watsonx.data Spark](/docs/watsonxdata?group=working-with-watsonxdata-spark).

## Supported Spark version for {{site.data.keyword.lakehouse_short}} Spark engine
{: #cpu-mem-spk_versn}


{{site.data.keyword.lakehouse_full}} supports the following Spark runtime versions to run Spark workloads by using {{site.data.keyword.lakehouse_short}}.

| Name | Status | Release date | End-of-support date |
| ------------ | ------------- | ------- | ---- |
| Apache Spark 3.4.4 | Deprecated | JUNE 2023 | JUNE 2026 |
| Apache Spark 3.5.4 | Supported | FEB 2025 | FEB 2028 |
| Apache Spark 4.0 | Supported | AUG 2025 | AUG 2028 |
{: caption="Supported Spark versions" caption-side="top"}
