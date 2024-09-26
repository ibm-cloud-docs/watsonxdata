---

copyright:
  years: 2017, 2024
lastupdated: "2024-09-24"

keywords: watsonx.data, spark, emr
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Presto exposed JMX metrics
{: #presto_expd_jmx}

This topic covers the Presto exposed JMX metrics with details.

## Alluxio cache metrics
{: #presto_expd_jmx_1}

| Metric name  |  Metric type  | Metric description  |
|--------------|---------------|---------------------|
| watsonx_data_presto_alluxio_cache_bytes_read_cache_count | Counter | Tracks the number of bytes read from Alluxio cache. |
| watsonx_data_presto_alluxio_cache_bytes_read_cache_fifteen_minute_rate | Gauge | Measures the rate of bytes read from Alluxio cache over fifteen minutes. |
| watsonx_data_presto_alluxio_cache_bytes_requested_external_count | Counter | Tracks the number of bytes requested externally from Alluxio cache. |
| watsonx_data_presto_alluxio_cache_bytes_requested_external_fifteen_minute_rate | Gauge | Measures the rate of bytes requested externally from Alluxio cache over fifteen minutes. |
| watsonx_data_presto_alluxio_cache_bytes_written_cache_fifteen_minute_rate | Gauge | Measures the rate of bytes written to Alluxio cache over fifteen minutes. |
| watsonx_data_presto_alluxio_cache_get_errors_count | Counter | Counts the number of errors that are encountered while getting data from Alluxio cache. |
| watsonx_data_presto_alluxio_cache_hit_rate_value | Gauge | Provides the hit rate of Alluxio cache. |
| watsonx_data_presto_alluxio_cache_pages_count | Counter | Tracks the number of pages in Alluxio cache. |
| watsonx_data_presto_alluxio_cache_pages_evicted_count | Counter | Counts the number of pages that are evicted from Alluxio cache. |
| watsonx_data_presto_alluxio_cache_pages_evicted_fifteen_minute_rate | Gauge | Measures the rate of pages that are evicted from Alluxio cache over fifteen minutes. |
| watsonx_data_presto_alluxio_cache_put_errors_count | Counter | Counts the number of errors that are encountered while putting data into Alluxio cache. |
| watsonx_data_presto_alluxio_cache_space_available_value | Gauge | Indicates the available space in Alluxio cache. |
| watsonx_data_presto_alluxio_cache_space_used_value | Gauge | Indicates the used space in Alluxio cache. |
| watsonx_data_presto_alluxio_cache_written_cache_external_count | Counter | Tracks the number of bytes written to external cache from Alluxio. |
{: caption="Table 1. Alluxio cache metrics" caption-side="bottom"}

## Presto cache CacheStats metrics
{: #presto_expd_jmx_2}

| Metric name  |  Metric type  | Metric description  |
|--------------|---------------|---------------------|
| watsonx_data_presto_cache_stats_cache_hit | Counter | Tracks the number of cache hits in Presto cache. |
| watsonx_data_presto_cache_stats_cache_miss | Counter | Tracks the number of cache misses in Presto cache. |
| watsonx_data_presto_cache_stats_in_memory_retained_bytes | Gauge | Indicates the number of bytes retained in memory in Presto cache. |
| watsonx_data_presto_cache_stats_quota_exceeded | Counter | Counts the instances where the cache quota is exceeded. |
{: caption="Table 2. Presto cache CacheStats metrics" caption-side="bottom"}

## Cluster-wide memory usage metrics
{: #presto_expd_jmx_3}

| Metric name  |  Metric type  | Metric description  |
|--------------|---------------|---------------------|
| watsonx_data_presto_cluster_memory_manager_queries_killed_due_to_out_of_memory | Counter | Tracks the number of queries killed due to out of memory errors. |
| watsonx_data_presto_cluster_memory_pool_general_assigned_queries | Gauge | Indicates the number of queries that are assigned to the general memory pool. |
| watsonx_data_presto_cluster_memory_pool_general_blocked_nodes | Gauge | Indicates the number of nodes that are blocked in the general memory pool. |
| watsonx_data_presto_cluster_memory_pool_general_free_distributed_bytes | Gauge | Indicates the number of free distributed bytes in the general memory pool. |
| watsonx_data_presto_cluster_memory_pool_general_total_distributed_bytes | Gauge | Indicates the total distributed bytes in the general memory pool. |
{: caption="Table 3. Cluster wide memory usage metrics" caption-side="bottom"}

## Fragment result cache metrics
{: #presto_expd_jmx_4}

| Metric name  |  Metric type  | Metric description  |
|--------------|---------------|---------------------|
| watsonx_data_presto_fragment_cache_stats_cache_entries | Counter | Tracks the number of cache entries in the fragment result cache. |
| watsonx_data_presto_fragment_cache_stats_cache_hit | Counter | Tracks the number of cache hits in the fragment result cache. |
| watsonx_data_presto_fragment_cache_stats_cache_removal | Counter | Tracks the number of cache removals in the fragment result cache. |
| watsonx_data_presto_fragment_cache_stats_cache_size_in_bytes | Gauge | Indicates the size of the fragment result cache in bytes. |
| watsonx_data_presto_fragment_cache_stats_inflight_bytes | Gauge | Indicates the number of inflight bytes in the fragment result cache. |
{: caption="Table 4. Cluster wide memory usage metrics" caption-side="bottom"}

## Java garbage collector metrics
{: #presto_expd_jmx_5}

| Metric name  |  Metric type  | Metric description  |
|--------------|---------------|---------------------|
| watsonx_data_presto_garbage_collector_global_collection_count | Counter | Tracks the number of global garbage collections. |
| watsonx_data_presto_garbage_collector_global_collection_time_milliseconds | Gauge | Measures the time spent in global garbage collection in milliseconds. |
| watsonx_data_presto_garbage_collector_scavenge_collection_count | Counter | Tracks the number of scavenge garbage collections. |
| watsonx_data_presto_garbage_collector_scavenge_collection_time_milliseconds | Gauge | Measures the time spent in scavenge garbage collection in milliseconds. |
{: caption="Table 5. Java garbage collector metrics" caption-side="bottom"}

## File metadata cache metrics
{: #presto_expd_jmx_6}

| Metric name  |  Metric type  | Metric description  |
|--------------|---------------|---------------------|
| watsonx_data_presto_hive_cache_stats_mbean_orc_file_tail_hit_rate | Gauge | Indicates the hit rate for ORC file tail metadata cache. |
| watsonx_data_presto_hive_cache_stats_mbean_orc_file_tail_size | Gauge | Indicates the size of the ORC file tail metadata cache. |
| watsonx_data_presto_hive_cache_stats_mbean_parquet_metadata_hit_rate | Gauge | Indicates the hit rate for Parquet metadata cache. |
| watsonx_data_presto_hive_cache_stats_mbean_parquet_metadata_size | Gauge | Indicates the size of the Parquet metadata cache. |
| watsonx_data_presto_hive_cache_stats_mbean_partition_hit_rate | Gauge | Indicates the hit rate for partition metadata cache. |
| watsonx_data_presto_hive_cache_stats_mbean_partition_size | Gauge | Indicates the size of the partition metadata cache. |
{: caption="Table 6. File metadata cache metrics" caption-side="bottom"}

## Java heap memory metrics
{: #presto_expd_jmx_7}

| Metric name  |  Metric type  | Metric description  |
|--------------|---------------|---------------------|
| watsonx_data_presto_memory_heap_memory_usage_committed_bytes | Gauge | Indicates the committed bytes in heap memory usage. |
| watsonx_data_presto_memory_heap_memory_usage_init_bytes | Gauge | Indicates the initial bytes in heap memory usage. |
| watsonx_data_presto_memory_heap_memory_usage_max_bytes | Gauge | Indicates the maximum bytes in heap memory usage. |
| watsonx_data_presto_memory_heap_memory_usage_used_bytes | Gauge | Indicates the used bytes in heap memory usage. |
{: caption="Table 7. Java heap memory metrics" caption-side="bottom"}

## Java non-heap memory metrics
{: #presto_expd_jmx_8}

| Metric name  |  Metric type  | Metric description  |
|--------------|---------------|---------------------|
| watsonx_data_presto_memory_non_heap_memory_usage_committed_bytes | Gauge | Indicates the committed bytes in non-heap memory usage. |
| watsonx_data_presto_memory_non_heap_memory_usage_init_bytes | Gauge | Indicates the initial bytes in non-heap memory usage. |
| watsonx_data_presto_memory_non_heap_memory_usage_max_bytes | Gauge | Indicates the maximum bytes in non-heap memory usage. |
| watsonx_data_presto_memory_non_heap_memory_usage_used_bytes | Gauge | Indicates the used bytes in non-heap memory usage. |
{: caption="Table 8. Java non-heap memory metrics" caption-side="bottom"}

## Java memory pool metrics
{: #presto_expd_jmx_9}

| Metric name  |  Metric type  | Metric description  |
|--------------|---------------|---------------------|
| watsonx_data_presto_memory_pool_MemoryPool_nursery_allocate_usage_committed_bytes | Gauge | Indicates the committed bytes in the nursery-allocate memory pool (equivalent to G1 Eden Space). |
| watsonx_data_presto_memory_pool_MemoryPool_nursery_allocate_usage_used_bytes | Gauge | Indicates the used bytes in the nursery-allocate memory pool (equivalent to G1 Eden Space). |
| watsonx_data_presto_memory_pool_MemoryPool_tenured_SOA_usage_committed_bytes | Gauge | Indicates the committed bytes in the tenured-SOA memory pool (equivalent to G1 Old Gen). |
| watsonx_data_presto_memory_pool_MemoryPool_tenured_SOA_usage_used_bytes | Gauge | Indicates the used bytes in the tenured-SOA memory pool (equivalent to G1 Old Gen). |
| watsonx_data_presto_memory_pool_MemoryPool_tenured_LOA_usage_committed_bytes | Gauge | Indicates the committed bytes in the tenured-LOA memory pool (equivalent to G1 Old Gen). |
| watsonx_data_presto_memory_pool_MemoryPool_tenured_LOA_usage_used_bytes | Gauge | Indicates the used bytes in the tenured-LOA memory pool (equivalent to G1 Old Gen). |
{: caption="Table 9. Java memory pool metrics" caption-side="bottom"}

## Presto memory pool metrics
{: #presto_expd_jmx_10}

| Metric name  |  Metric type  | Metric description  |
|--------------|---------------|---------------------|
| watsonx_data_presto_memory_pool_general_free_bytes | Gauge | Indicates the number of free bytes in the general memory pool. |
| watsonx_data_presto_memory_pool_general_max_bytes | Gauge | Indicates the maximum number of bytes in the general memory pool. |
| watsonx_data_presto_memory_pool_general_reserved_bytes | Gauge | Indicates the number of reserved bytes in the general memory pool. |
| watsonx_data_presto_memory_pool_general_reserved_revocable_bytes | Gauge | Indicates the number of reserved revocable bytes in the general memory pool. |
| watsonx_data_presto_memory_pool_general_total_bytes | Gauge | Indicates the total number of bytes in the general memory pool. |
{: caption="Table 10. Presto memory pool metrics" caption-side="bottom"}

## Scheduler metrics
{: #presto_expd_jmx_11}

| Metric name  |  Metric type  | Metric description  |
|--------------|---------------|---------------------|
| watsonx_data_presto_node_selection_stats_non_preferred_node_selected_count_total_count     | Counter     | Total count of times a non-preferred node was selected by the scheduler.                                     |
| watsonx_data_presto_node_selection_stats_non_primary_preferred_node_selected_count_total_count | Counter     | Total count of times a non-primary preferred node was selected by the scheduler.                             |
| watsonx_data_presto_node_selection_stats_primary_preferred_node_selected_count_five_minute_rate | Gauge       | Rate of times a primary preferred node was selected by the scheduler over the last five minutes.             |
| watsonx_data_presto_node_selection_stats_primary_preferred_node_selected_count_total_count | Counter     | Total count of times a primary preferred node was selected by the scheduler.                                 |
{: caption="Table 11. Scheduler metrics" caption-side="bottom"}

## Airlift stats pause meter metrics
{: #presto_expd_jmx_12}

| Metric name  |  Metric type  | Metric description  |
|--------------|---------------|---------------------|
| watsonx_data_presto_pause_meter_less_than_10ms_pauses                              | Counter     | Total count of pauses lasting less than 10 milliseconds.                                                     |
| watsonx_data_presto_pause_meter_10ms_to_50ms_pauses                                | Counter     | Total count of pauses lasting between 10 and 50 milliseconds.                                                |
| watsonx_data_presto_pause_meter_50ms_to_500ms_pauses                               | Counter     | Total count of pauses lasting between 50 and 500 milliseconds.                                               |
| watsonx_data_presto_pause_meter_500ms_to_1s_pauses                                 | Counter     | Total count of pauses lasting between 500 milliseconds and 1 second.                                         |
| watsonx_data_presto_pause_meter_1s_to_10s_pauses                                   | Counter     | Total count of pauses lasting between 1 and 10 seconds.                                                      |
| watsonx_data_presto_pause_meter_10s_to_1m_pauses                                   | Counter     | Total count of pauses lasting between 10 seconds and 1 minute.                                               |
| watsonx_data_presto_pause_meter_greater_than_1m_pauses                             | Counter     | Total count of pauses lasting greater than 1 minute.                                                         |
| watsonx_data_presto_pause_meter_total_pause_seconds                                | Counter     | Total count of all pause seconds.                                                                            |
{: caption="Table 12. Airlift stats pause meter metrics" caption-side="bottom"}

## Presto execution query manager metrics
{: #presto_expd_jmx_13}

| Metric name  |  Metric type  | Metric description  |
|--------------|---------------|---------------------|
| watsonx_data_presto_query_manager_abandoned_queries_five_minute_count              | Counter     | Count of queries abandoned in the last five minutes.                                                         |
| watsonx_data_presto_query_manager_canceled_queries_five_minute_count               | Counter     | Count of queries canceled in the last five minutes.                                                          |
| watsonx_data_presto_query_manager_completed_queries_five_minute_count              | Counter     | Count of queries completed in the last five minutes.                                                         |
| watsonx_data_presto_query_manager_consumed_cpu_time_seconds_five_minute_count      | Counter     | Count of CPU time consumed in seconds in the last five minutes.                                              |
| watsonx_data_presto_query_manager_consumed_input_bytes_five_minute_count           | Counter     | Count of input bytes consumed in the last five minutes.                                                      |
| watsonx_data_presto_query_manager_consumed_input_rows_five_minute_count            | Counter     | Count of input rows consumed in the last five minutes.                                                       |
| watsonx_data_presto_query_manager_cpu_input_byte_rate_five_minutes_p$1             | Gauge       | Rate of CPU input bytes in the last five minutes.                                                            |
| watsonx_data_presto_query_manager_execution_time_five_minutes_p$1                  | Gauge       | Execution time in the last five minutes.                                                                     |
| watsonx_data_presto_query_manager_external_failures_five_minute_count              | Counter     | Count of external query failures in the last five minutes.                                                   |
| watsonx_data_presto_query_manager_failed_queries_five_minute_count                 | Counter     | Count of failed queries in the last five minutes.                                                            |
| watsonx_data_presto_query_manager_insufficient_resources_failures_five_minute_count | Counter    | Count of queries that failed due to insufficient resources in the last five minutes.                         |
| watsonx_data_presto_query_manager_internal_failures_five_minute_count              | Counter     | Count of internal query failures in the last five minutes.                                                   |
| watsonx_data_presto_query_manager_queued_queries                                   | Gauge       | Number of queries currently queued.                                                                          |
| watsonx_data_presto_query_manager_queued_time_five_minutes_p$1                     | Gauge       | Time queries spent in queue in the last five minutes.                                                        |
| watsonx_data_presto_query_manager_running_queries                                  | Gauge       | Number of queries currently running.                                                                         |
| watsonx_data_presto_query_manager_started_queries_five_minute_count                | Counter     | Count of queries started in the last five minutes.                                                           |
| watsonx_data_presto_query_manager_submitted_queries_five_minute_count              | Counter     | Count of queries submitted in the last five minutes.                                                         |
| watsonx_data_presto_query_manager_user_error_failures_five_minute_count            | Counter     | Count of queries that failed due to user errors in the last five minutes.                                     |
| watsonx_data_presto_query_manager_wall_input_bytes_rate_five_minutes_p$1           | Gauge       | Rate of wall input bytes in the last five minutes.                                                           |
{: caption="Table 13. Presto execution query manager metrics" caption-side="bottom"}

## Java lang runtime metrics
{: #presto_expd_jmx_14}

| Metric name  |  Metric type  | Metric description  |
|--------------|---------------|---------------------|
| watsonx_data_presto_runtime_up_time                                                | Gauge       | Uptime of the Java runtime.                                                                                  |
{: caption="Table 14. Java lang runtime metrics" caption-side="bottom"}

## Presto execution scheduler SplitSchedulerStats metrics
{: #presto_expd_jmx_15}

| Metric name  |  Metric type  | Metric description  |
|--------------|---------------|---------------------|
| watsonx_data_presto_split_scheduler_stats_get_split_time_five_minutes_p$1          | Gauge       | Get split time in the last five minutes.                                                                     |
| watsonx_data_presto_split_scheduler_stats_mixed_split_queues_full_and_waiting_for_source_five_minute_count | Counter | Count of mixed split queues that are full and waiting for source in the last five minutes.                   |
| watsonx_data_presto_split_scheduler_stats_sleep_time_five_minutes_p$1              | Gauge       | Sleep time in the last five minutes.                                                                         |
| watsonx_data_presto_split_scheduler_stats_split_queues_full_five_minute_count      | Counter     | Count of split queues that are full in the last five minutes.                                                |
| watsonx_data_presto_split_scheduler_stats_waiting_for_source_five_minute_count     | Counter     | Count of waiting for source events in the last five minutes.                                                 |
{: caption="Table 15. Presto execution scheduler SplitSchedulerStats metrics" caption-side="bottom"}

## Presto execution executor TaskExecutor metrics
{: #presto_expd_jmx_16}

| Metric name  |  Metric type  | Metric description  |
|--------------|---------------|---------------------|
| watsonx_data_presto_task_executor_$1                                               | Gauge       | Metrics related to the task executor. Attributes: ActiveTasks, BlockedTasks, CompletedTasks, CorePoolSize, CurrentThreadCount, ExecutedTasks, ExecutorUtilization, FailedTasks, LargestPoolSize, MaximumPoolSize, MinimumIdleThreads, MinimumThreadCount, PendingTasks, PoolSize, QueueSize, TaskCount, TaskExecutionTime, ThreadCount, TotalExecutionTime, UtilizationRate |
{: caption="Table 16. Presto execution executor TaskExecutor metrics" caption-side="bottom"}

## Presto execution task manager metrics
{: #presto_expd_jmx_17}

| Metric name  |  Metric type  | Metric description  |
|--------------|---------------|---------------------|
| watsonx_data_presto_task_manager_failed_tasks_five_minute_count                    | Counter     | Count of failed tasks in the last five minutes.                                                              |
| watsonx_data_presto_task_manager_input_data_size_five_minute_count                 | Counter     | Count of input data size in the last five minutes.                                                           |
| watsonx_data_presto_task_manager_input_positions_five_minute_count                 | Counter     | Count of input positions in the last five minutes.                                                           |
| watsonx_data_presto_task_manager_output_data_size_five_minute_count                | Counter     | Count of output data size in the last five minutes.                                                          |
| watsonx_data_presto_task_manager_output_positions_five_minute_count                | Counter     | Count of output positions in the last five minutes.                                                          |
{: caption="Table 17. Presto execution task manager metrics" caption-side="bottom"}

## Java NIO buffer pool metrics
{: #presto_expd_jmx_18}

| Metric name  |  Metric type  | Metric description  |
|--------------|---------------|---------------------|
| watsonx_data_presto_java_nio_buffer_pool__$1_memory_used                           | Gauge       | Memory used by the Java NIO buffer pool.                                                                   |
{: caption="Table 18. Java NIO buffer pool metrics" caption-side="bottom"}

## Presto dispatcher metrics
{: #presto_expd_jmx_19}

| Metric name  |  Metric type  | Metric description  |
|--------------|---------------|---------------------|
| watsonx_data_presto_dispatch_manager_queued_queries                                | Gauge       | Count of queries queued in the Presto dispatcher.                                                            |
| watsonx_data_presto_dispatch_manager_running_queries                               | Gauge       | Count of queries currently running in the Presto dispatcher.                                                 |
{: caption="Table 19. Presto dispatcher metrics" caption-side="bottom"}

## Glue stats metrics
{: #presto_expd_jmx_20}

| Metric name  |  Metric type  | Metric description  |
|--------------|---------------|---------------------|
| watsonx_data_presto_glue_$2_time_$3_$4                                             | Gauge       | Time taken by Glue Hive Metastore operations.                  |
| watsonx_data_presto_glue_$2_total_failures_total_count                             | Counter     | Total count of failures for Glue Hive Metastore operations.                                 |
| watsonx_data_presto_glue_$2_total_failures_fifteen_minute_$3                       | Gauge (rate), Counter (count) | Rate or count of failures for Glue Hive Metastore operations in the last fifteen minutes.           |
{: caption="Table 20. Glue stats metrics" caption-side="bottom"}

## S3 file system metrics
{: #presto_expd_jmx_21}

| Metric name  |  Metric type  | Metric description  |
|--------------|---------------|---------------------|
| watsonx_data_presto_hive_s3_presto_s3_file_system_$2_$3_$4                         | Gauge (rate), Counter (count) | Metrics related to the S3 file system in Presto Hive.            |
| watsonx_data_presto_hive_s3_presto_s3_file_system_$2_total_count                   | Counter     | Total count metric related to the S3 file system in Presto Hive.                              |
| watsonx_data_presto_s3_$2_$3_$4                                                    | Gauge (avg, max, min, maxerror), Counter (count), other (unit) | Additional metrics related to S3 operations.        |
{: caption="Table 21. S3 file system metrics" caption-side="bottom"}

## Hive directory list caching metrics
{: #presto_expd_jmx_22}

| Metric name  |  Metric type  | Metric description  |
|--------------|---------------|---------------------|
| watsonx_data_presto_hive_caching_directory_lister_$2                               | Gauge       | Metrics related to the caching directory lister in Presto Hive.                                              |
{: caption="Table 22. Hive directory list caching metrics" caption-side="bottom"}

## Parquet metadata caching metrics
{: #presto_expd_jmx_23}

| Metric name  |  Metric type  | Metric description  |
|--------------|---------------|---------------------|
| watsonx_data_presto_hive_cache_stats_mbean_parquet_metadata_eviction_count         | Counter     | Eviction count related to Parquet metadata caching in Presto Hive.                                           |
{: caption="Table 23. Parquet metadata caching metrics" caption-side="bottom"}
