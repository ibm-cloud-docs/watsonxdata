---

copyright:
  years: 2017, 2024
lastupdated: "2024-10-28"

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
| `async-data-cache-enabled` | Boolean | True or False |
| `query-reserved-memory-gb` | Integer | Limit {1, 1000} |
| `system-mem-limit-gb` | Integer | Limit {1, 1e13} |
| `system-mem-shrink-gb` | Integer | Limit {1, 1e13} |
| `system-mem-pushback-enabled` | Boolean | True or False |
{: caption="Configuration properties for Presto (C++) - worker nodes" caption-side="bottom"}

 If the `system-mem-pushback-enabled` property is set to `true`, the default limit of `system-mem-limit-gb` will not be enough. It is recommended to set the value of `system-mem-limit-gb` same as `system-memory-gb`.
 {: note}

## Properties to be customized under support guidance
{: #api_custom_sprt_pcpp}

Though most of the properties can be customized by the watsonx.data administrators, the following properties must be customized under the guidance of the {{site.data.keyword.lakehouse_short}} support team.

| Property name | Type | Validation added |
| --- | --- | --- |
| `runtime-metrics-collection-enabled` | Boolean | True or False |
| `system-mem-pushback-enabled` | Boolean | True or False |
| `system-mem-limit-gb` | Integer | Limit{1, 100000} |
| `system-mem-shrink-gb` | Integer | Limit{1, 100000} |
{: caption="Properties to be customized under support guidance" caption-side="bottom"}
