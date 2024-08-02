---

copyright:
  years: 2017, 2024
lastupdated: "2024-08-02"

keywords: watsonx.data, spark, emr
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Configuration properties for Presto (C++) - coordinator nodes
{: #aapi_custom_pcpp_cood}

You can customize the coordinator configuration properties through an API for Presto (C++).

| Property name | Type | Validation added |
| --- | --- | --- |
| `http-server.log.max-size` | String | Limit {1, 1e13}; supported values are numbers with or without units TB, MB, GB, B, KB |
| `http-server.log.max-history` | Integer | Limit {1, 1000} |
| `http-server.threads.max` | Integer | Limit {1, 1000} |
| `log.max-history` | Integer | Limit {1, 1000} |
| `log.max-size` | String | Limit {1, 1e13}; supported values are numbers with or without units TB, MB, GB, B, KB |
| `node-scheduler.max-pending-splits-per-task` | Integer | Limit {1, 1000} |
| `node-scheduler.max-splits-per-node` | Integer | Limit {1, 1000} |
| `optimizer.joins-not-null-inference-strategy` | String | Any string |
| `optimizer.default-filter-factor-enabled` | Boolean |  True or False |
| `optimizer.exploit-constraints` | Boolean | True or False |
| `optimizer.in-predicates-as-inner-joins-enabled` | Boolean | True or False |
| `optimizer.partial-aggregation-strategy` | String | Any string |
| `optimizer.prefer-partial-aggregation` | Boolean | True or False |
| `optimizer.infer-inequality-predicates` | Boolean | True or False |
| `optimizer.handle-complex-equi-joins` | Boolean | True or False |
| `optimizer.generate-domain-filters` | Boolean | True or False |
| `optimizer.size-based-join-flipping-enabled` | Boolean | True or False |
| `join-max-broadcast-table-size` | String | Limit {1, 1e13}; supported values are numbers with or without units TB, MB, GB, B, KB |
| `query.client.timeout` | String | Limit {1, 1e13}; supported values are numbers with or without units m, s, ms, h |
| `query.execution-policy` | String | Any string |
| `query.low-memory-killer.policy` | String | Any string |
| `query.max-execution-time` | String | Limit {1, 1e13}; supported values are numbers with or without units m,s,ms,h |
| `query.max-history` | Integer | Limit {1, 10000} |
| `query.max-total-memory-per-node` | String | Limit {1, 1e13}; supported values are numbers with or without units TB, MB, GB, B, KB |
| `query.max-total-memory` | String | Limit {1, 1e13}; supported values are numbers with or without units TB, MB, GB, B, KB |
| `query.max-memory-per-node` | String | Limit {1, 1e13}; supported values are numbers with or without units TB, MB, GB, B, KB |
| `query.max-memory` | String | Limit {1, 1e13} supported values are numbers with or without units TB, MB, GB, B, KB |
| `query.max-stage-count` | Integer | Limit {1, 10000} |
| `query.min-expire-age` | String | supported values are numbers with or without units m, s, ms, h |
| `query.min-schedule-split-batch-size` | Integer | Limit {1, 10000} |
| `query.stage-count-warning-threshold` | Integer | Limit {1, 10000} |
| `query.max-length` | Integer | Limit {1, 10000} |
| `scale-writers` | Boolean | True or False |
| `scheduler.http-client.max-requests-queued-per-destination` | Integer | Limit {1, 100000} |
| `shutdown.grace-period` | String | Limit {1, 1e13}; supported values are numbers with or without units m, s, ms, h |
{: caption="Table 1. Configuration properties for Presto (C++) - coordinator nodes" caption-side="bottom"}
