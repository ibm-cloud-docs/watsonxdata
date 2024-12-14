---

copyright:
  years: 2017, 2024
lastupdated: "2024-12-07"

keywords: watsonx.data, spark, emr
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# JVM properties for Presto (C++) - coordinator nodes
{: #api_custom_jvm_pcpp}

You can customize the coordinator JVM properties through an API for Presto (C++).

| Property name | Type | Validation added |
| --- | --- | --- |
| `-XX:G1HeapRegionSize` | String | Limit {1, 1e13}; supported values are numbers with or without units TB, MB, GB, B, KB, M, G, B |
| `-XX:ReservedCodeCacheSize` | String | Limit {1, 1e13}; supported values are numbers with or without units TB, MB, GB, B, KB, M, G, B |
| `-Djdk.nio.maxCachedBufferSize` | Integer | Limit {1, 1e13} |
| `-Dalluxio.user.app.id` | String | Any string |
| `-Duser.timezone` | String | Any string |
| `-xgc` | String | Any string |
| `-Xmx` | String | Any string |
|`-Xms` | String | Any string |
{: caption="JVM properties for Presto (C++) - coordinator nodes" caption-side="bottom"}