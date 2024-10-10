---

copyright:
  years: 2017, 2024
lastupdated: "2024-10-10"

keywords: watsonx.data, spark, emr
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# JVM properties for Presto (Java) - coordinator and worker nodes
{: #api_custom_jvm_pjcw}

You can customize the coordinator and worker JVM properties through an API for Presto (Java).

| Property name | Type | Validation added |
| --- | --- | --- |
| `-XX:G1HeapRegionSize` | String | Limit {1, 1e13}; supported values are numbers with or without units TB, MB, GB, B, KB, M, G, B |
| `-XX:ReservedCodeCacheSize` | String | Limit {1, 1e13}; supported values are numbers with or without units TB, MB, GB, B, KB, M, G, B |
| `-Djdk.nio.maxCachedBufferSize` | Integer | Limit {1, 1e13} |
| `-Dalluxio.user.app.id` | String | Any string |
| `-Duser.timezone` | String | Any string |
| `-xgc` | String | Any string |
| `-Xmx6G` | String | Any string |
{: caption="JVM properties for Presto (Java) - coordinator and worker nodes" caption-side="bottom"}
