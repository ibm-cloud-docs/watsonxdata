---

copyright:
  years: 2022, 2024
lastupdated: "2024-08-05"

keywords: watsonxdata, qhmm

subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}


# Monitoring and managing diagnostic data
{: #mon_mng}

Query History Monitoring and Management (QHMM) is a service that stores and manages the diagnostic data such as queries history and query event-related information of the Presto engine in the Minio bucket, {{site.data.keyword.lakehouse_short}}. You can retrieve the stored history files for analysis, debugging and monitoring purpose.
The Query history monitoring and management page in {{site.data.keyword.lakehouse_short}} provides information for fetching the history data and analyzing the queries that are run.
{: shortdesc}

## Before you begin
{: #mon_mng_bgn}

Ensure that you have the following information:
- `<instance-id>`: unique identifier of the watsonx.data instance. Save the instance ID for reference.
- `<engine>` : the engine used for data processing. Here, Presto.
- `<catalog>`: the catalog specific to QHMM. Save the catalog name for reference. Here we use, wxd_system_data.
- `<bucket>` : the MinIO bucket for storing the diagnostic data. Save the bucket name for reference. Here we use, wxd-system.

Go to the Query workspace page and do the following:

1. Run the following command to create a schema to organize the diagnostic data for QHMM.

```bash
CREATE SCHEMA IF NOT EXISTS <catalog>.diag WITH (location = 's3a://wxd-system/diag/');
```
{: codeblock}

Here, the <catalog> name is wxd_system_data.

2. Run the following command to create a table to store the query event data.

```bash
CREATE TABLE IF NOT EXISTS <catalog>.diag.query_event_raw (
  record VARCHAR,
  dt VARCHAR
)
WITH (
  external_location = 's3a://<bucket>/qhmm/<instance-id>/<engine>/<engine-id>/QueryEvent/',
  format = 'textfile',
  partitioned_by = ARRAY['dt']
);
```
{: codeblock}

Here, the <catalog> name is wxd_system_data.

3. Run the following command to create a table to store the query history data in JSON format.

```bash
CREATE TABLE IF NOT EXISTS <catalog>.diag.query_history(
  query_id VARCHAR,
  query VARCHAR,
  state VARCHAR,
  source VARCHAR,
  created VARCHAR,
  started VARCHAR,
  "end" VARCHAR,
  dt VARCHAR,
  user VARCHAR)
WITH (
  external_location = 's3a://<bucket>/qhmm/<instance-id>/<engine>/<engine-id>/QueryHistory/',
  format = 'JSON',
  partitioned_by = ARRAY['dt','user']
);
```
{: codeblock}

Here, the <catalog> name is wxd_system_data.

## Procedure
{: #gen_qhmm-pro}

The system stores the data in watsonx.data MinIO buckets. Here, wxd-system.

The system removes the data after every 7 days, and the maximum storage capacity is 1 GB (exceeding limit trims the data to fit into 1 GB size).
{: note}

1. Log in to IBM watsonx.data console.

1. Go to the Objects tab in the minIO bucket page. The query table displays the QueryEvent and QueryHistory folders with data files in JSON format.

1. Synchronizing with the QHMM data

    a. From the navigation menu, go to the Query workspace page.

    b. Run the following command to fetch the current QHMM data into the watsonx.data table.

    ```bash
    USE <catalog>.diag;
    CALL system.sync_partition_metadata('diag', 'query_event_raw', 'FULL');
    CALL system.sync_partition_metadata('diag', 'query_history', 'FULL');
    ```
    {: codeblock}

1. To view data that is fetched from QHMM, run the following command:


    ```bash
    CREATE VIEW <catalog>.diag.query_event_view AS
    SELECT
    json_extract_scalar (record, '$.clusterName') cluster_name,
    json_extract_scalar (record, '$.queryCompletedEvent.metadata.queryId') query_id,
    json_extract_scalar (
        record,
        '$.queryCompletedEvent.metadata.queryState'
    ) query_state,
    CAST(
        json_extract (record, '$.queryCompletedEvent.ioMetadata.inputs') AS JSON
    ) query_inputs,
    from_unixtime (
        CAST(
            json_extract_scalar (
                record,
                '$.queryCompletedEvent.createTime.epochSecond'
            ) AS bigint
        )
    ) create_time,
    from_unixtime (
        CAST(
            json_extract_scalar (
                record,
                '$.queryCompletedEvent.executionStartTime.epochSecond'
            ) AS bigint
        )
    ) execution_start_time,
    from_unixtime (
        CAST(
            json_extract_scalar (
                record,
                '$.queryCompletedEvent.endTime.epochSecond'
            ) AS bigint
        )
    ) end_time,
    json_extract_scalar (record, '$.cpuTimeMillis') cpuTimeMillis,
    json_extract_scalar (record, '$.wallTimeMillis') wallTimeMillis,
    json_extract_scalar (record, '$.queuedTimeMillis') queuedTimeMillis,
    json_extract_scalar (record, '$.analysisTimeMillis') analysisTimeMillis,
    (
        CAST(
            json_extract (
                record,
                '$.queryCompletedEvent.statistics.planningTime.seconds'
            ) AS BIGINT
        ) * 1000 + CAST(
            json_extract (
                record,
                '$.queryCompletedEvent.statistics.planningTime.nano'
            ) AS BIGINT
        ) / 1000000
    ) planningTimeMillis,
    json_extract_scalar (record, '$.queryCompletedEvent.context.user') user,
    CAST(
        "json_extract" (record, '$.queryCompletedEvent.stageStatistics') AS ARRAY (ROW (gcStatistics MAP (VARCHAR, INTEGER)))
    ) gcStatistics,
    json_extract_scalar (
        record,
        '$.queryCompletedEvent.statistics.totalRows'
    ) total_rows,
    json_extract_scalar (
        record,
        '$.queryCompletedEvent.statistics.outputRows'
    ) output_rows,
    json_extract_scalar (
        record,
        '$.queryCompletedEvent.statistics.writtenOutputRows'
    ) written_output_rows,
    json_extract_scalar (
        record,
        '$.queryCompletedEvent.statistics.totalBytes'
    ) total_bytes,
    json_extract_scalar (
        record,
        '$.queryCompletedEvent.statistics.outputBytes'
    ) output_bytes,
    json_extract_scalar (
        record,
        '$.queryCompletedEvent.statistics.cumulativeMemory'
    ) cumulative_memory,
    json_extract_scalar (
        record,
        '$.queryCompletedEvent.statistics.completedSplits'
    ) completed_splits,
    json_extract_scalar (
        record,
        '$.queryCompletedEvent.statistics.peakRunningTasks'
    ) peak_running_tasks,
    json_extract_scalar (
        record,
        '$.queryCompletedEvent.statistics.peakUserMemoryBytes'
    ) peak_user_memory_bytes,
    json_extract_scalar (
        record,
        '$.queryCompletedEvent.statistics.peakTotalNonRevocableMemoryBytes'
    ) peak_total_non_revocable_memory_bytes,
    json_extract_scalar (
        record,
        '$.queryCompletedEvent.statistics.peakTaskUserMemory'
    ) peak_task_user_memory,
    json_extract_scalar (
        record,
        '$.queryCompletedEvent.statistics.peakTaskTotalMemory'
    ) peak_task_total_memory,
    json_extract_scalar (
        record,
        '$.queryCompletedEvent.statistics.peakNodeTotalMemory'
    ) peak_node_total_memory,
    json_extract_scalar (record, '$.queryCompletedEvent.context.source') source,
    json_extract_scalar (record, '$.queryCompletedEvent.context.catalog') catalog,
    json_extract_scalar (record, '$.queryCompletedEvent.context.schema') schema,
    CAST(
        json_extract (
            record,
            '$.queryCompletedEvent.context.resourceGroupId'
        ) AS ARRAY (VARCHAR)
    ) resource_group_id,
    CAST(
        json_extract (
            record,
            '$.queryCompletedEvent.context.sessionProperties'
        ) AS MAP (VARCHAR, VARCHAR)
    ) session_properties,
    json_extract_scalar (
        record,
        '$.queryCompletedEvent.context.serverVersion'
    ) server_version,
    CAST(
        "json_extract" (
            record,
            '$.queryCompletedEvent.failureInfo.errorCode'
        ) AS MAP (VARCHAR, VARCHAR)
    ) error_code,
    json_extract_scalar (
        record,
        '$.queryCompletedEvent.failureInfo.failureType'
    ) failure_type,
    json_extract_scalar (
        record,
        '$.queryCompletedEvent.failureInfo.failureMessage'
    ) failure_message,
    json_extract_scalar (
        record,
        '$.queryCompletedEvent.failureInfo.failuresJson'
    ) failure_json,
    json_extract_scalar (record, '$.plan') plan,
    json_extract_scalar (record, '$.queryCompletedEvent.metadata.query') query,
    regexp_like("json_extract_scalar"(record, '$.plan'), 'InnerJoin|RightJoin|SemiJoin|CrossJoin|FullJoin') isAJoinQuery
    FROM
    <catalog>.diag.query_event_raw
    ```
    {: codeblock}

1. To can analyze the statistics and memory usage information and view the garbage code details, run the following command:

    ```bash
    CREATE VIEW <catalog>.diag.fullGC_TaskDetails AS
    SELECT
        query_id,
        create_time,
        execution_start_time,
        end_time,
        SUM(i."gcStatistics"['tasks']) as total_tasks,
        SUM(i."gcStatistics"['fullGcTasks']) total_full_gc_tasks,
        SUM(i."gcStatistics"['maxFullGcSec']) max_full_gc_sec,
        SUM(i."gcStatistics"['totalFullGcSec']) total_full_gc_sec,
        b.gcStatistics,
        query,
        isAJoinQuery
    FROM
      <catalog>.diag.query_event_view b
      CROSS JOIN UNNEST(b.gcStatistics) WITH ORDINALITY AS i ("gcStatistics", n)
      GROUP BY query_id, create_time, execution_start_time, end_time, b.gcStatistics, query, isAJoinQuery;
    ```
    {: codeblock}

1. To view query statistics and memory usage, run the following command:

    ```bash
    CREATE VIEW <catalog>.diag.table_stats_information_memory AS (
    SELECT catalogname, schema, "table", isAJoinQuery, row_count_stats, total_size_stats, execution_start_time, peak_node_total_memory,
    CASE
    WHEN row_count_stats != 'NaN' OR total_size_stats != 'NaN' THEN 'YES'
    ELSE 'NO'
    END AS is_table_stats_available
    FROM (
      SELECT json_extract_scalar(i.statistics['totalSize'], '$.value') total_size_stats,
             json_extract_scalar(i.statistics['rowCount'], '$.value') row_count_stats,
             i.n, i.schema, i."table", i.catalogName, b.execution_start_time, b.peak_node_total_memory, b.isAJoinQuery
      FROM <catalog>.diag.query_event_view b
    cross join
      UNNEST(CAST(b.query_inputs AS Array(ROW(catalogName VARCHAR, schema VARCHAR, "table" VARCHAR, statistics MAP(VARCHAR, JSON)))))
      WITH ORDINALITY AS i (catalogName, schema, "table", statistics, n))
    );
    ```
    {: codeblock}

1. To run the SQL commands sequentially in your SQL environment to analyze the data that is fetched, run the following command:

    ```bash
    SELECT * FROM  <catalog>.diag.query_event_raw limit 10;
    -- To check partitions
    SELECT * FROM  <catalog>.diag."query_event_raw$partitions";

    SELECT * from <catalog>.diag.query_event_view where query_state='FINISHED' limit 10;
    SELECT * from <catalog>.diag.fullGC_TaskDetails limit 10;
    SELECT * from <catalog>.diag.table_stats_information_memory limit 10;
    ```
    {: codeblock}
