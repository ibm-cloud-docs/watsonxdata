---

copyright:
  years: 2022, 2025
lastupdated: "2026-04-07"

keywords: watsonx.data, data ingestion, source file

subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Ingesting streaming data by using Spark Stream (Experimental)
{: #ingest_spark_stream}

You can ingest real-time streaming data into {{site.data.keyword.lakehouse_full}} by using the Spark Stream ingestion flow. This experimental feature enables you to configure streaming sources and continuously ingest data into target tables.

This feature is experimental and subject to change. It is not recommended for production use.
{: note}

## Before you begin
{: #ingest_spark_stream1}

- Review the [prerequisites](/docs/watsonxdata?topic=watsonxdata-ingest_spark_ui#ingest_spark_ui3) for using the Spark ingestion UI.
- Create the target schema and table before you start the streaming job.
- Streaming sources must be pre-configured by administrators. Contact your administrator if no streaming sources are available.
- An API key is required for streaming jobs.

## Procedure
{: #ingest_spark_stream2}

1. Log in to the {{site.data.keyword.lakehouse_short}} console.
2. From the navigation menu, select **Data manager**.
3. Click **Ingest data**.
4. Select **Spark Stream [Experimental]** as the ingestion flow.
5. In the **Source configuration** section:

   1. **Streaming source**: Select a streaming source from the dropdown.

   2. **Topic**: Enter the topic name for the streaming source.

6. In the **Streaming configuration** section:

   1. **Trigger interval (seconds)**: Specify how often the streaming query should run (default: 15 seconds).

   2. **Starting offsets (optional)**: Specify where to start reading from the stream.

   3. **Max offsets per trigger (optional)**: Limit the number of offsets to process per trigger.

   4. **Max retries**: Specify the maximum number of retry attempts for failed operations (default: 5).

   5. **Retry delay (seconds)**: Specify the delay between retry attempts (default: 60 seconds).

   6. **Fail on data loss**: Toggle to control behavior when data loss is detected.
      - **Disabled**: Continue processing even if data loss is detected
      - **Enabled**: Fail the job if data loss is detected

   7. **Stop gracefully on shutdown**: Toggle to control shutdown behavior.
      - **Enabled** (default): Stop the streaming job gracefully, ensuring all in-flight data is processed
      - **Disabled**: Stop immediately without waiting for in-flight data

7. In the **Target table** section:

   1. **Select catalog**: Choose the target catalog from the dropdown.

   2. **Select schema**: Choose the target schema from the dropdown.

   3. **Select table**: Choose the target table from the dropdown.

   The schema and table must exist before starting the streaming job, and the table schema must be compatible with the streaming data schema.
   {: note}

8. In the **Job details** section:

   1. **Job ID**: A unique job identifier is automatically generated.

   2. **API key (required for streaming jobs)**: Enter an API key for authentication.

   3. **Select engine**: Choose the Spark engine to use for the streaming job from the dropdown.

9. Click **Submit** to start the streaming job, or **Cancel** to discard the configuration.

## Results
{: #ingest_spark_stream3}

While the streaming job is running, data from the streaming source is continuously ingested into the target table. The job continues running until manually stopped or until it encounters an error.

Unlike batch ingestion jobs, streaming jobs run continuously. Monitor the job regularly and stop it when no longer needed to avoid unnecessary resource usage.
{: note}

## Stopping the streaming job
{: #ingest_spark_stream4}

To stop a running streaming job:

1. Navigate to **Data manager** > **View jobs**.
2. Locate your streaming job in the list.
3. Click **Stop job** or use the job management controls.

## Related information
{: #ingest_spark_stream5}

- [Ingesting data by using the Spark ingestion UI](/docs/watsonxdata?topic=watsonxdata-ingest_spark_ui)
- [Ingesting data from local system](/docs/watsonxdata?topic=watsonxdata-ingest_spark_local)
- [Ingesting data from remote storage](/docs/watsonxdata?topic=watsonxdata-ingest_spark_storage)
- [Ingesting data from remote database](/docs/watsonxdata?topic=watsonxdata-ingest_spark_database)
- [Ingesting data from Delta Lake to Iceberg tables](/docs/watsonxdata?topic=watsonxdata-ingest_spark_deltalake)
