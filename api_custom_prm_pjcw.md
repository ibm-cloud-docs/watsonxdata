---

copyright:
  years: 2017, 2024
lastupdated: "2024-12-11"

keywords: watsonx.data, spark, emr
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Configuration properties for Presto (Java) - coordinator and worker nodes
{: #api_custom_prm_pjcw}

You can customize the coordinator and worker configuration properties through an API for Presto (Java).

| Property name | Type | Validation added |
| --- | --- | --- |
| `experimental.optimized-repartitioning` | Boolean | True or False |
| `experimental.reserved-pool-enabled` | Boolean | True or False |
| `fragment-result-cache.enabled` | Boolean | True or False |
| `fragment-result-cache.max-cached-entries` | Integer | `1000000` |
| `fragment-result-cache.base-directory` | String | file:///mnt/tmpfs/fragment |
| `fragment-result-cache.cache-ttl` | String | 24h |
| `heap_dump_on_exceeded_memory_limit.enabled` | Boolean | True or False |
| `heap_dump_on_exceeded_memory_limit.file_directory` | String | Any string |
| `heap_dump_on_exceeded_memory_limit.max.number` | Integer | Limit {1, 1000} |
| `heap_dump_on_exceeded_memory_limit.max.size` | Integer | Limit {1, 1000} |
| `memory.heap-headroom-per-node` | String | Limit {1, 1e9}; supported values are numbers with or without units TB, MB, GB, B, KB |
| `node-scheduler.include-coordinator` | Boolean | True or False |
| `query.execution-policy` | String | Any string |
| `query.low-memory-killer.policy` | String | Any string |
| `query.max-memory` | String | Limit {1, 1e13}; supported values are numbers with or without units TB, MB, GB, B, KB |
| `query.max-memory-per-node` | String | Limit {1, 1e13}; supported values are numbers with or without units TB, MB, GB, B, KB |
| `query.max-stage-count` | Integer | Limit {1, 1000} |
| `query.max-total-memory-per-node` | String | Limit {1, 1e13}; supported values are numbers with or without units TB, MB, GB, B, KB |
| `query.min-expire-age` | String | Limit {1, 1e13}; supported values are numbers with or without units m, s, ms, h |
| `query.stage-count-warning-threshold` | Integer | Limit {1, 1000} |
| `task.concurrency` | Integer | Limit {1, 1000} |
| `task.max-drivers-per-task` | Integer | Limit {1, 100} |
| `join-distribution-type` | String | Value should be automatic or broadcast or partitioned |
| `exchange.client-threads` | Integer | Limit {1, 1000} |
| `exchange.http-client.max-connections` | Integer | Limit {1, 10000} |
| `exchange.http-client.max-connections-per-server` | Integer | Limit {1, 100000} |
| `http-server.log.max-size` | String | Limit {1, 1e13}; supported values are numbers with or without units TB, MB, GB, B, KB |
| `http-server.log.max-history` | Integer | Limit {1, 100} |
| `http-server.threads.max` | Integer | Limit {1, 1000} |
| `join-max-broadcast-table-size` | String | Limit {1, 1e13}; supported values are numbers with or without units TB, MB, GB, B, KB |
| `log.max-history` | Integer | Limit {1, 100} |
| `log.max-size` | String | Limit {1, 1e13}; supported values are numbers with or without units TB, MB, GB, B, KB |
| `node-scheduler.max-pending-splits-per-task` | Integer | Limit {1, 3000} |
| `node-scheduler.max-splits-per-node` | Integer | Limit {1, 3000} |
| `optimize-nulls-in-join` | Boolean | True or False |
| `optimizer.default-filter-factor-enabled` | Boolean | True or False |
| `optimizer.exploit-constraints` | Boolean | True or False |
| `optimizer.prefer-partial-aggregation` | Boolean | True or False |
| `query.client.timeout` | String | Limit {1, 1e13}; supported values are numbers with or without units m, s, ms, h |
| `query.max-execution-time` | String | Limit {1, 1e13}; supported values are numbers with or without units m, s, ms, h |
| `query.max-history` | Integer | Limit {1, 100} |
| `query.max-total-memory` | String | Limit {1, 1e13}; supported values are numbers with or without units TB, MB, GB|
| `query.min-schedule-split-batch-size` | String | Limit {1, 1e13}; supported values are numbers with or without units TB, MB, GB, B, KB |
| `query.max-length` | Integer | Limit {1, 1000000} |
| `scale-writers` | Boolean | True or False |
| `shutdown.grace-period` | String | Limit {1, 1e13}; supported values are numbers with or without units m, s, ms, h |
| `sink.max-buffer-size` | String | Limit {1, 1e13}; supported values are numbers with or without units TB, MB, GB, B, KB |
| `experimental.max-revocable-memory-per-node` | String | Limit {1, 1e13}; supported values are numbers with or without units TB, MB, GB, B, KB |
| `experimental.max-spill-per-node` | String | Limit {1, 1e13}; supported values are numbers with or without units TB, MB, GB, B, KB |
| `experimental.pushdown-dereference-enabled` | Boolean | True or False |
| `experimental.pushdown-subfields-enabled` | Boolean | True or False |
| `experimental.query-max-spill-per-node` | String | Limit {1, 1e13}; supported values are numbers with or without units TB, MB, GB, B, KB |
| `experimental.spiller-max-used-space-threshold` | Float | Float 64 |
| `experimental.spiller-spill-path` | String | Any string |
| `http-server.max-request-header-size` | String | Limit {1, 1e13}; supported values are numbers with or without units TB, MB, GB, B, kB |
| `http-server.max-response-header-size` | String | Limit {1, 1e13}; supported values are numbers with or without units TB, MB, GB, B, kB |
| `experimental.internal-communication.max-task-update-size` | String | Limit {1, 1e13}; supported values are numbers with or without units TB, MB, GB, B, KB |
|`offset-clause-enabled`|Boolean|True or False |
{: caption="Configuration properties for Presto (Java) - coordinator and worker nodes" caption-side="bottom"}

To enable fragment cache, you must set up a cache-enabled environment. To set up, patch the following properties into `/opt/presto/etc/config.properties`.

```bash
fragment-result-cache.enabled: true
fragment-result-cache.base-directory: file:///mnt/tmpfs/fragment
fragment-result-cache.max-cached-entries: 1000000
fragment-result-cache.cache-ttl: 24h
```
{: codeblock}

The mount path `/mnt/tmpfs/fragment` is by default available on a cache-enabled environment with the system's volume mounted on it.
