---

copyright:
  years: 2017, 2024
lastupdated: "2024-07-03"

keywords: watsonx.data, spark, emr
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Configuration properties for Presto (C++) - worker nodes
{: #api_custom_wkr_pcpp}

You can customize the worker configuration properties through an API for Presto (C++).

| Property name | Type | Validation added |
| --- | --- | --- |
| `task.max-drivers-per-task` | Integer | Limit {1, 100} |
| `system-memory-gb` | Integer | Limit {1, 1000} |
| `query-memory-gb` | Integer | Limit {1, 10000} |
| `query.max-memory-per-node` | Integer | Limit {1, 1000} |
| `async-data-cache-enabled` | Boolean | True or false values |
| `query-reserved-memory-gb` | Integer | Limit {1, 1000} |
{: caption="Table 1. Configuration properties for Presto (C++) - worker nodes" caption-side="bottom"}

## Properties to be customized under support guidance
{: #api_custom_sprt_pcpp}

Though most of the properties can be customized by the watsonx.data administrators, the following properties must be customized under the guidance of the {{site.data.keyword.lakehouse_short}} support team.

| Property name | Type | Validation added |
| --- | --- | --- |
| `runtime-metrics-collection-enabled` | Boolean | True or false values |
| `system-mem-pushback-enabled` | Boolean | True or false values |
| `system-mem-limit-gb` | Integer | Limit{1, 100000} |
| `system-mem-shrink-gb` | Integer | Limit{1, 100000} |
{: caption="Table 2. Properties to be customized under support guidance" caption-side="bottom"}
