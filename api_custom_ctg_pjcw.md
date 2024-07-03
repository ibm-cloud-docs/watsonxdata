---

copyright:
  years: 2017, 2024
lastupdated: "2024-07-03"

keywords: watsonx.data, spark, emr
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Catalog properties for Presto (Java)
{: #api_custom_ctg_pjcw}

You can customize the catalog properties through an API for Presto (Java).

| Property name | Type | Validation added |
| --- | --- | --- |
| `cache.enabled` | Boolean | True or false values |
| `cache.base-directory` | String | Any string |
| `cache.type` | String | Any string |
| `cache.alluxio.max-cache-size` | String | Limit {1, 1e13}; supported values are numbers with or without units TB, MB, GB, B, KB |
| `hive.partition-statistics-based-optimization-enabled` | Boolean | True or false values |
| `hive.metastore-cache-scope` | String | Any string |
| `hive.metastore-cache-ttl` | String | Limit {1, 1e13}; supported values are numbers with or without units m, s, ms, h |
| `hive.metastore-refreshInterval` | String | Limit {1, 1e13}; supported values are numbers with or without units m, s, ms, h, d |
| `hive.metastore-cache-maximum-size` | Integer | Limit {1, 1000} |
| `hive.partition-versioning-enabled` | Boolean | True or false values |
| `hive.file-status-cache-expire-time` | String | Limit {1, 1e13}; supported values are numbers with or without units m, s, ms, h |
| `hive.file-status-cache-size` | Integer | Limit {1, 10000000000} |
| `hive.file-status-cache-tables` | String | Any string |
| `<catalog-name>.orc.file-tail-cache-enabled` | Boolean | True or false values |
| `<catalog-name>.orc.file-tail-cache-size` | Integer | Limit{1, 1000000} |
| `<catalog-name>.orc.file-tail-cache-ttl-since-last-access` | String | Limit {1, 1e13}; supported values are numbers with or without units m, s, ms, h |
| `<catalog-name>.orc.stripe-metadata-cache-enabled` | Boolean | True or false values |
| `<catalog-name>.orc.stripe-footer-cache-size` | Integer | Limit {1, 1000} |
| `<catalog-name>.orc.stripe-footer-cache-ttl-since-last-access` | String | Limit {1, 1e13}; supported values are numbers with or without units m, s, ms, h |
| `<catalog-name>.orc.stripe-stream-cache-size` | Integer | Limit {1, 1000} |
| `<catalog-name>.orc.stripe-stream-cache-ttl-since-last-access` | String | Limit {1, 1e13}; supported values are numbers with or without units m, s, ms, h |
| `hive.orc.use-column-names` | True | True or false values |
| `<catalog-name>.parquet.metadata-cache-enabled` | True | True or false values |
| `<catalog-name>.parquet.metadata-cache-size` | Integer | Limit {1, 1000} |
| `<catalog-name>.parquet.metadata-cache-ttl-since-last-access` | String | Limit {1, 1e13}; supported values are numbers with or without units m, s, ms, h |
| `hive.parquet.use-column-names` | True | True or false values |
| `hive.parquet-batch-read-optimization-enabled` | True | True or false values |
| `hive.node-selection-strategy` | String | Any string |
| `hive.max-outstanding-splits` | Integer | Limit {1, 1000} |
| `hive.max-initial-splits` | Integer | Limit {1, 1000} |
| `hive.max-initial-split-size` | Integer | Limit {1, 1000} |
| `hive.max-split-size` | Integer | Limit {1, 1000} |
| `hive.split-loader-concurrency` | Integer | Limit {1, 1000} |
| `hive.pushdown-filter-enabled` | Boolean | True or false values |
| `hive.max-partitions-per-writers` | Integer | Limit {1, 1000} |
| `hive.s3.max-error-retries` | Integer | Limit {1, 100} |
| `hive.s3.connect-timeout` | String | Limit {1, 1e13}; supported values are numbers with or without units m, s, ms, h |
| `hive.s3.socket-timeout` | String | Limit {1, 1e13}; supported values are numbers with or without units m, s, ms, h |
| `hive.s3.max-connections` | Integer | Limit {1, 10000} |
| `hive.s3.max-client-retries` | Integer | Limit {1, 100} |
| `hive.collect-column-statistics-on-write` | Boolean | True or false values |
| `hive.non-managed-table-creates-enabled` | Boolean | True or false values |
| `hive.s3select-pushdown.enabled` | Boolean | True or false values |
| `hive.recursive-directories` | Boolean | True or false values |
| `hive.allow-rename-table` | Boolean | True or false values |
| `hive.allow-add-column` | Boolean | True or false values |
| `hive.allow-drop-column` | Boolean | True or false values |
| `hive.allow-rename-column` | Boolean | True or false values |
| `hive.metastore-timeout` | String | Limit {1, 1e13}; supported values are numbers with or without units m, s, ms, h |
{: caption="Table 1. Catalog properties for Presto (Java)" caption-side="bottom"}
