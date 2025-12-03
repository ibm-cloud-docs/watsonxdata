---

copyright:
  years: 2022, 2025
lastupdated: "2025-12-03"

keywords: watsonx.data, Presto, Milvus, dashboards, observability, metrics

subcollection: watsonxdata

---

{:javascript: #javascript .ph data-hd-programlang='javascript'}
{:java: #java .ph data-hd-programlang='java'}
{:ruby: #ruby .ph data-hd-programlang='ruby'}
{:php: #php .ph data-hd-programlang='php'}
{:python: #python .ph data-hd-programlang='python'}
{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:video: .video}


# Supporting dashboards
{: #opntlmtry_inst_dash2}

{{site.data.keyword.lakehouse_full}} Presto (Java) offer comprehensive observability through a robust set of dashboards that provide visibility into performance metrics, enabling rapid issue diagnosis and optimizing resource allocation.

The following are the supported dashboards:
- System health
- Query performance health
- Data and metadata health
- Workload health
- Query latency health
- Query lifecycle health
- Anomaly and trend insights
- Log and error health

The Grafana tool provides support only for the following four dashboards System health, Query performance health, Data and metadata health, and Workload health while the Instana tool supports all the eight dashboards.
{: note}

The following list represents the default set of Presto (Java) metrics. Users can extend this by adding additional metrics as needed. A full list of available metrics and their definitions can be found in [Presto exposed JMX metrics](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-presto_expd_jmx){: external}.
{: note}

## System health
{: #opntlmtry_inst_dash2_syshlth}

Monitoring the underlying infrastructure is paramount for Presto. Focuses on the foundational infrastructure, monitoring core resources like CPU, memory, and I/O to detect bottlenecks and ensure stable operations.

**Presto (Java) engine:**

- **CPU usage** - Monitors CPU usage across Presto instances.
   - `process_cpu_seconds_total`

- **Memory usage** - Tracks total memory used versus available
   - `watsonx_data_presto_cluster_memory_manager_cluster_memory_bytes`
   - `watsonx_data_presto_cluster_memory_manager_leaked_bytes`
   - `watsonx_data_presto_memory_heap_memory_usage_committed_bytes`
   - `watsonx_data_presto_memory_heap_memory_usage_max_bytes`
   - `watsonx_data_presto_memory_non_heap_memory_usage_committed_bytes`
   - `watsonx_data_presto_memory_non_heap_memory_usage_max_bytes`
   - `watsonx_data_presto_cluster_memory_manager_cluster_user_memory_reservation`
   - `watsonx_data_presto_cluster_memory_manager_cluster_total_memory_reservation`
   - `watsonx_data_presto_cluster_memory_manager_queries_killed_due_to_out_of_memory`
   - `jvm_memory_bytes_committed`

- **Presto memory pool** - Tracks memory consumption within the reserved and general memory pools of Presto.
   - `watsonx_data_presto_memory_pool_general_max_bytes`
   - `watsonx_data_presto_cluster_memory_pool_general_nodes`
   - `watsonx_data_presto_memory_pool_general_free_bytes`
   - `watsonx_data_presto_memory_pool_general_reserved_bytes`
   - `watsonx_data_presto_cluster_memory_pool_general_free_distributed_bytes`
   - `watsonx_data_presto_cluster_memory_pool_general_total_distributed_bytes`
   - `watsonx_data_presto_cluster_memory_pool_general_reserved_distributed_bytes`
   - `watsonx_data_presto_cluster_memory_pool_general_reserved_revocable_distributed_bytes`

- **Alluxio cache** - Tracks the efficiency and usage of cached data in Alluxio during queries.
   - `watsonx_data_presto_alluxio_cache_bytes_read_cache_count`
   - `watsonx_data_presto_alluxio_cache_bytes_requested_external_count`
   - `watsonx_data_presto_alluxio_cache_written_cache_external_count`
   - `watsonx_data_presto_alluxio_cache_get_errors_count`
   - `watsonx_data_presto_alluxio_cache_put_errors_count`
   - `watsonx_data_presto_alluxio_cache_pages_count`
   - `watsonx_data_presto_alluxio_cache_pages_evicted_count`
   - `watsonx_data_presto_alluxio_cache_space_available_value`
   - `watsonx_data_presto_alluxio_cache_space_used_value`

To generate Alluxio cache metrics, the Alluxio cache must be enabled. For more information, refer to [Enhancing the query performance through caching](https://www.ibm.com/docs/en/software-hub/5.2.x?topic=administering-enhancing-query-performance-through-caching){: external}
{: note}

Additionally, ensure the following configurations are included in the `jvm.config` file:
`-Dalluxio.metrics.key.including.unique.id.enabled=true`
`-Dalluxio.user.app.id=presto`

- **Fragment cache** - Tracks usage and hit or miss rates of cached query fragments in Presto.
   - `watsonx_data_presto_fragment_cache_stats_cache_entries`
   - `watsonx_data_presto_fragment_cache_stats_cache_hit`
   - `watsonx_data_presto_fragment_cache_stats_cache_removal`
   - `watsonx_data_presto_fragment_cache_stats_cache_size_in_bytes`
   - `watsonx_data_presto_fragment_cache_stats_inflight_bytes`

## Query performance
{: #opntlmtry_inst_dash2_qryperf}

Understanding query behavior is critical for a query engine. Query performance metrics include:

**Presto (Java) engine:**

- **Currently running queries** - Monitors the query request rate.
   - `watsonx_data_presto_query_manager_running_queries`

- **Query execution time** - Tracks query latency.
   - `watsonx_data_presto_query_manager_execution_time_five_minutes_p99`

- **Data processed** - Measures data transfer rates during query execution.
   - `watsonx_data_presto_task_manager_input_data_size_five_minute_count`
   - `watsonx_data_presto_task_manager_output_data_size_five_minute_count`

- **Error rates** - Indicates the percentage of queries that error out when the system is under stress.
   - `watsonx_data_presto_query_manager_user_error_failures_five_minute_count`
   - `watsonx_data_presto_query_manager_abandoned_queries_five_minute_count`
   - `watsonx_data_presto_query_manager_canceled_queries_five_minute_count`

- **Successful vs failed requests** - Tracks successful vs failed request counts.
   - `watsonx_data_presto_query_manager_completed_queries_five_minute_count`
   - `watsonx_data_presto_query_manager_failed_queries_five_minute_count`
   - `watsonx_data_presto_query_manager_internal_failures_five_minute_count`
   - `watsonx_data_presto_task_manager_failed_tasks_five_minute_count`

## Data and metadata health
{: #opntlmtry_inst_dash2_metadatahlth}

For a system dealing with vast amounts of data, the health of data ingestion and metadata management is crucial.

**Presto (Java) engine:**

- **Data ingestion - Query manager** - Monitors the volume and rate of data being ingested into the system.
   - `watsonx_data_presto_query_manager_consumed_input_bytes_five_minute_count`
   - `watsonx_data_presto_query_manager_consumed_input_rows_five_minute_count`
   - `watsonx_data_presto_query_manager_wall_input_bytes_rate_five_minutes_p90`

- **S3 Object store errors** - Tracks failure metrics while reading data from S3 or object storage layers.
   - `watsonx_data_presto_hive_s3_presto_s3_file_system_get_metadata_errors_total_count`
   - `watsonx_data_presto_hive_s3_presto_s3_file_system_failed_uploads_total_count`
   - `watsonx_data_presto_hive_s3_presto_s3_file_system_other_read_errors_total_count`

- **Queue metric** - Measures the size and processing rate of internal data processing queues.
   - `watsonx_data_presto_dispatch_manager_queued_queries`
   - `watsonx_data_presto_split_scheduler_stats_mixed_split_queues_full_and_waiting_for_source_five_minute_count`
   - `watsonx_data_presto_task_executor_processor_executor_queued_task_count`
   - `watsonx_data_presto_task_executor_split_queued_time_all_time_max`
   - `watsonx_data_presto_task_executor_split_queued_time_all_time_avg`

- **File metadata cache metrics** - Observes hit/miss rates and efficiency of the metadata cache for file access.
   - `watsonx_data_presto_hive_cache_stats_mbean_parquet_metadata_hit_rate`
   - `watsonx_data_presto_hive_cache_stats_mbean_parquet_metadata_size`
   - `watsonx_data_presto_hive_cache_stats_mbean_orc_file_tail_size`
   - `watsonx_data_presto_hive_cache_stats_mbean_orc_file_tail_hit_rate`
   - `watsonx_data_presto_hive_cache_stats_mbean_stripe_footer_size`
   - `watsonx_data_presto_hive_cache_stats_mbean_stripe_stream_size`

## Workload health
{: #opntlmtry_inst_dash2_wrkldhlth}

Understanding how different workloads interact with the system is key to resource optimization.

**Presto (Java) engine:**

- **Workload count** - Indicates the number of currently running queries.
   - `watsonx_data_presto_query_manager_running_queries`

- **Status** - Indicates whether the workload is active, idle, or failed.
   - `watsonx_data_presto_query_manager_completed_queries_five_minute_count`
   - `watsonx_data_presto_query_manager_abandoned_queries_five_minute_count`
   - `watsonx_data_presto_query_manager_canceled_queries_five_minute_count`
   - `watsonx_data_presto_query_manager_failed_queries_five_minute_count`

- **Error rates** - Error rates
   - `watsonx_data_presto_query_manager_user_error_failures_five_minute_count`
   - `watsonx_data_presto_query_manager_failed_queries_five_minute_count`
   - `watsonx_data_presto_query_manager_external_failures_five_minute_count`
   - `watsonx_data_presto_query_manager_internal_failures_five_minute_count`
   - `watsonx_data_presto_query_manager_insufficient_resources_failures_five_minute_count`

- **Resource utilization** - Tracks CPU, memory, and disk usage associated with each workload.
   - `watsonx_data_presto_query_manager_consumed_cpu_time_seconds_five_minute_count`
   - `watsonx_data_presto_query_manager_cpu_input_byte_rate_five_minutes_p25`
   - `watsonx_data_presto_query_manager_cpu_input_byte_rate_five_minutes_p50`
   - `watsonx_data_presto_query_manager_cpu_input_byte_rate_five_minutes_p75`
   - `watsonx_data_presto_query_manager_cpu_input_byte_rate_five_minutes_p90`

- **Request count** - Total number of workload execution requests received over a period of time.
   - `watsonx_data_presto_query_manager_running_queries`
   - `watsonx_data_presto_dispatch_manager_queued_queries`

## Query lifecycle health
{: #opntlmtry_inst_dash2_qrylfcyclhlth}

It provides insight into each stage of a query’s journey from submission to execution helping to identify bottlenecks in queuing, task execution, and completion.

**Presto (Java) engine:**

- **Errors in each stage** - Tracks query execution failures across different stages of the Presto instances by identifying the problem areas in the pipeline where tasks are failing.
   - `watsonx_data_presto_task_manager_failed_tasks_five_minute_count`

- **Resource utilization per query** - Captures system resource usage per query, including threads, splits, and queued or executing queries.
   - `watsonx_data_presto_task_executor_running_tasks_level0`
   - `watsonx_data_presto_task_executor_running_splits`
   - `watsonx_data_presto_query_manager_submitted_queries_five_minute_count`
   - `watsonx_data_presto_query_manager_queued_queries`
   - `watsonx_data_presto_dispatch_manager_queued_queries`
   - `watsonx_data_presto_task_executor_blocked_splits`

- **Executor pool health** - Monitors the internal thread pool used to run Presto tasks.
   - `watsonx_data_presto_task_executor_processor_executor_pool_size`
   - `watsonx_data_presto_task_executor_processor_executor_active_count`
   - `watsonx_data_presto_task_executor_processor_executor_completed_task_count`
   - `watsonx_data_presto_task_executor_processor_executor_queued_task_count`

- **Split CPU time** - Tracks CPU time consumed by leaf and intermediate splits.
   - `watsonx_data_presto_task_executor_intermediate_split_cpu_time_count`
   - `watsonx_data_presto_query_manager_consumed_cpu_time_seconds_five_minute_count`
   - `watsonx_data_presto_task_executor_leaf_split_cpu_time_p99`

## Query latency health
{: #opntlmtry_inst_dash2_qryltncyhlth}

Focuses on the execution phase of queries identifying latency sources and the impact of query complexity.

**Presto (Java) engine:**

- **Latency (ms)** - Measures execution time across various stages.
   - `watsonx_data_presto_query_manager_execution_time_five_minutes_p99`
   - `watsonx_data_presto_task_executor_split_wall_time_one_minute_max`
   - `watsonx_data_presto_task_executor_split_wall_time_fifteen_minutes_max`
   - `watsonx_data_presto_task_executor_split_wall_time_all_time_p99`
   - `watsonx_data_presto_task_executor_leaf_split_wall_time_p99`

- **Request Volume** - Tracks task, split, and scheduling activity.
   - `watsonx_data_presto_task_executor_split_queued_time_five_minutes_count`
   - `watsonx_data_presto_split_scheduler_stats_get_split_time_five_minutes_p99`
   - `watsonx_data_presto_task_executor_split_wall_time_five_minutes_count`

## Log and error health
{: #opntlmtry_inst_dash2_logerrhlth}

Monitors errors and failures across the query execution pipeline, highlighting system stability and failure patterns.

**Presto (Java) engine:**

- **Query failure rate** - Tracks execution failures and bottlenecks.
   - `watsonx_data_presto_query_manager_failed_queries_five_minute_count`
   - `watsonx_data_presto_query_manager_internal_failures_five_minute_count`
   - `watsonx_data_presto_query_manager_user_error_failures_five_minute_count`
   - `watsonx_data_presto_task_executor_split_skipped_due_to_memory_pressure_five_minute_count`

- **Service/component affected - Hive S3 / FileSystem** - Identifies failing Presto components.
   - `watsonx_data_presto_hive_s3_presto_s3_file_system_failed_uploads_total_count`
   - `watsonx_data_presto_hive_s3_presto_s3_file_system_aws_retry_count_fifteen_minute_count`
   - `watsonx_data_presto_hive_s3_presto_s3_file_system_get_metadata_errors_total_count`
   - `watsonx_data_presto_hive_s3_presto_s3_file_system_socket_timeout_exceptions_total_count`

- **Service/component affected - Task Executor** - Identifies failing Presto components.
   - `watsonx_data_presto_task_executor_split_wall_time_all_time_max_error`
   - `watsonx_data_presto_task_executor_blocked_quanta_wall_time_all_time_max_error`
   - `watsonx_data_presto_task_executor_leaf_split_cpu_time_max_error`
   - `watsonx_data_presto_task_executor_intermediate_split_wall_time_max_error`
   - `watsonx_data_presto_task_executor_unblocked_quanta_wall_time_one_minute_max_error`
   - `watsonx_data_presto_task_executor_split_queued_time_one_minute_max_error`
   - `watsonx_data_presto_hive_s3_presto_s3_file_system_failed_uploads_total_count`
   - `watsonx_data_presto_hive_s3_presto_s3_file_system_aws_retry_count_fifteen_minute_count`
   - `watsonx_data_presto_hive_s3_presto_s3_file_system_get_metadata_errors_total_count`
   - `watsonx_data_presto_hive_s3_presto_s3_file_system_socket_timeout_exceptions_total_count`

- **Severity level** - Categorizes metrics by impact severity.

   - **Severe (Critical)**
      - `watsonx_data_presto_query_manager_internal_failures_five_minute_count`
      - `watsonx_data_presto_task_executor_split_wall_time_all_time_max_error`
      - `watsonx_data_presto_task_executor_blocked_quanta_wall_time_all_time_max_error`
      - `watsonx_data_presto_hive_s3_presto_s3_file_system_failed_uploads_total_count`
      - `watsonx_data_presto_cache_stats_quota_exceeded`

   - **Moderate (Warning)**
      - `watsonx_data_presto_query_manager_user_error_failures_five_minute_count`
      - `watsonx_data_presto_hive_s3_presto_s3_file_system_aws_retry_count_fifteen_minute_rate`
      - `watsonx_data_presto_hive_s3_presto_s3_file_system_get_object_errors_fifteen_minute_rate`
      - `watsonx_data_presto_hive_s3_presto_s3_file_system_read_retries_fifteen_minute_rate`
   - **Low (Info)**
      - `watsonx_data_presto_hive_s3_presto_s3_file_system_get_metadata_retries_five_minute_count`
      - `watsonx_data_presto_task_executor_split_skipped_due_to_memory_pressure_total_count`
      - `watsonx_data_presto_task_executor_processor_executor_shutdown`

## Anomaly and trend insights
{: #opntlmtry_inst_dash2_anmlytrnd}

Highlights unexpected patterns or deviations in query behavior, helping detect performance degradation or improvements.

**Presto (Java) engine:**

- **Latency drift** - Tracks evolving query latencies.
   - `watsonx_data_presto_task_executor_split_wall_time_fifteen_minutes_avg`
   - `watsonx_data_presto_task_executor_leaf_split_wait_time_avg`
   - `watsonx_data_presto_task_executor_intermediate_split_wall_time_avg`

- **Error rate vs baseline** - Compares recent execution metrics to historical baselines.
   - `watsonx_data_presto_task_executor_split_wall_time_fifteen_minutes_avg`
   - `watsonx_data_presto_task_executor_leaf_split_wait_time_avg`
   - `watsonx_data_presto_task_executor_intermediate_split_wall_time_avg`

- **Throughput drop detector** - Detects dips in data processing rates.
   - `watsonx_data_presto_task_executor_global_scheduled_time_micros_five_minute_rate`
   - `watsonx_data_presto_hive_s3_presto_s3_file_system_successful_uploads_five_minute_rate`

- **Query duration** - Measures average execution time per task or split.
   - `watsonx_data_presto_task_executor_leaf_split_cpu_time_avg`
   - `watsonx_data_presto_task_executor_intermediate_split_cpu_time_avg`

- **Memory trend** - Tracks memory usage and potential leaks.
   - `jvm_memory_bytes_used`
   - `watsonx_data_presto_memory_heap_memory_usage_used_bytes`

- **Workload trend comparison** - Compares resource usage across time windows.
   - `watsonx_data_presto_task_executor_global_cpu_time_micros_total_count`
   - `watsonx_data_presto_cluster_memory_manager_cluster_total_memory_reservation`
   - `watsonx_data_presto_task_executor_blocked_quanta_wall_time_fifteen_minutes_avg`
