---

copyright:
  years: 2022, 2026
lastupdated: "2026-04-07"

keywords: {{site.data.keyword.lakehouse_short}}, data ingestion, source file

subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Ingesting data from a local system
{: #ingest_spark_local}

You can upload files from your local system and ingest them into {{site.data.keyword.lakehouse_full}} by using the Spark ingestion UI.

## Before you begin
{: #ingest_spark_local1}

- Review the [prerequisites](/docs/watsonxdata?topic=watsonxdata-ingest_spark_ui#ingest_spark_ui3) for using the Spark ingestion UI.
- A transient storage bucket must be configured in your {{site.data.keyword.lakehouse_short}} instance for temporary file storage.
- The maximum cumulative file size for local uploads is 2 GB and individual file sizes must not exceed 200 MB limit. For larger files, use the [remote storage ingestion flow](/docs/watsonxdata?topic=watsonxdata-ingest_spark_storage).
- Lite ingestion of files smaller than 2 MB does not require a Spark engine. For files 2 MB or larger, you must provision a Spark engine before ingestion.
- Only one file type is supported per ingestion job.

## Supported file formats
{: #ingest_spark_local2}

- CSV (Comma-Separated Values)
- TXT
- Parquet
- JSON (JavaScript Object Notation)
- Avro
- ORC (Optimized Row Columnar)

## Procedure
{: #ingest_spark_local3}

1. Log in to the {{site.data.keyword.lakehouse_short}} console.
2. From the navigation menu, select **Data manager**.
3. Click **Ingest data**.
4. Select **Local system** as the ingestion flow.
5. In the top right corner of the page, select a transient storage bucket from the **Select transient storage bucket** dropdown.
6. This bucket will temporarily store your uploaded files during the ingestion process.
7. Click **Browse** or drag and drop your file into the upload area.
10. After the upload completes, the file name and size are displayed.
11. To upload additional files of the same type, click **Upload another file**.
12. Click **Next** to proceed to file details configuration.
13. Review the detected file format. If incorrect, select the correct format from the **File format** list.
14. Configure format-specific options:

   * For CSV and TXT files:

      - **Delimiter**: Specify the delimiter character (default: comma)
      - **Header**: Select whether the first row contains column headers
      - **Infer schema**: Enable to automatically detect column data types
      - **Quote character**: Specify the character used for quoting values (default: double quote)
      - **Escape character**: Specify the character used for escaping special characters (default: backslash)

   * For JSON files:

      - **Multi-line**: Enable if each JSON record spans multiple lines
      - **Infer schema**: Enable to automatically detect the schema from the JSON structure

   * For Parquet, Avro, and ORC files:

      - Schema is automatically detected from the file metadata

15. Click **Preview data** to view a sample of the data with the current configuration.
16. Verify that the data is parsed correctly. If not, adjust the configuration options.
17. Click **Next** to proceed to target table configuration.
18. See [Configuring target table settings](/docs/watsonxdata?topic=watsonxdata-ingest_spark_ui#ingest_spark_ui6) in the parent topic.
19. See [Configuring job details](/docs/watsonxdata?topic=watsonxdata-ingest_spark_ui#ingest_spark_ui7) in the parent topic.
20. Review the ingestion configuration summary.
22. Click **Submit** to start the ingestion job.

## Results
{: #ingest_spark_local4}

After the ingestion job completes successfully, the data from your local file is loaded into the target table. The uploaded file is stored temporarily and is automatically deleted after the ingestion job completes.

## Related information
{: #ingest_spark_local5}

- [Ingesting data by using the Spark ingestion UI](/docs/watsonxdata?topic=watsonxdata-ingest_spark_ui)
- [Ingesting data from remote storage](/docs/watsonxdata?topic=watsonxdata-ingest_spark_storage)
- [Ingesting data from remote database](/docs/watsonxdata?topic=watsonxdata-ingest_spark_database)
- [Ingesting data from Delta Lake to Iceberg tables](/docs/watsonxdata?topic=watsonxdata-ingest_spark_deltalake)
- [Ingesting streaming data by using Spark Stream (Experimental)](/docs/watsonxdata?topic=watsonxdata-ingest_spark_stream)
