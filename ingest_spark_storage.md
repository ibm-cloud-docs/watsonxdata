---

copyright:
  years: 2022, 2025
lastupdated: "2026-04-06"

keywords: {{site.data.keyword.lakehouse_short}}, data ingestion, source file

subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Ingesting data from remote storage
{: #ingest_spark_storage}

You can ingest data from remote storage systems into {{site.data.keyword.lakehouse_full}} by using the Spark ingestion UI. This flow supports cloud storage platforms such as Amazon S3, IBM Cloud Object Storage, and MinIO.

## Before you begin
{: #ingest_spark_storage1}

- Review the [prerequisites](/docs/watsonxdata?topic=watsonxdata-ingest_spark_ui#ingest_spark_ui3) for using the Spark ingestion UI.
- Ensure that the source storage system is accessible from the {{site.data.keyword.lakehouse_short}} environment.
- Have the appropriate credentials and permissions to access the storage system.

## Supported storage systems
{: #ingest_spark_storage2}

- Amazon S3
- IBM Cloud Object Storage
- Azure Data Lake Storage (ADLS)
- Google Cloud Storage (GCS)
- MinIO
- S3-compatible storage systems

## Supported file formats
{: #ingest_spark_storage3}

- CSV (Comma-Separated Values)
- TXT
- Parquet
- JSON (JavaScript Object Notation)
- Avro
- ORC (Optimized Row Columnar)

## Procedure
{: #ingest_spark_storage4}

1. Log in to the {{site.data.keyword.lakehouse_short}} console.
2. From the navigation menu, select **Data manager**.
3. Click **Ingest data**.
4. Select **Storages** as the ingestion flow.
5. From the **Select storage** dropdown, choose an existing storage connection, or click **Add +** to add a new storage connection.
6. If adding a new storage connection, select the **Storage type** and enter the connection details as per [Add Storage](/docs/watsonxdata?topic=watsonxdata-reg_bucket).
7. The file selection interface has two tabs:
   - **All files**: Displays all files in the selected storage bucket
   - **Selected files**: Shows only the files you have selected for ingestion
8. Browse the bucket contents to locate and select the files you want to ingest.
10. Switch to the **Selected files** tab to review your selections.
11. Click **Next** to proceed to file details configuration.

   You can select multiple files for batch ingestion. All selected files must have the same format and schema.
   {: note}

12. Review the detected file format. If incorrect, select the correct format from the **File format** list.
13. Configure format-specific options:

   **For CSV and TXT files:**

      - **Delimiter**: Specify the delimiter character (default: comma)
      - **Header**: Select whether the first row contains column headers
      - **Infer schema**: Enable to automatically detect column data types
      - **Quote character**: Specify the character used for quoting values (default: double quote)
      - **Escape character**: Specify the character used for escaping special characters (default: backslash)

   **For JSON files:**

      - **Multi-line**: Enable if each JSON record spans multiple lines
      - **Infer schema**: Enable to automatically detect the schema from the JSON structure

   **For Parquet, Avro, and ORC files:**

      - Schema is automatically detected from the file metadata

14. Click **Preview data** to view a sample of the data with the current configuration.
15. Verify that the data is parsed correctly. If not, adjust the configuration options.
16. Click **Next** to proceed to target table configuration.
17. See [Configuring target table settings](/docs/watsonxdata?topic=watsonxdata-ingest_spark_ui#ingest_spark_ui6) in the parent topic.
18. See [Configuring job details](/docs/watsonxdata?topic=watsonxdata-ingest_spark_ui#ingest_spark_ui7) in the parent topic.
19. Review the ingestion configuration summary.
20. Verify that all settings are correct.
21. Click **Submit** to start the ingestion job.

## Results
{: #ingest_spark_storage5}

After the ingestion job completes successfully, the data from the remote storage files is loaded into the target table. The source files remain in the remote storage bucket and are not modified.

## Related information
{: #ingest_spark_storage6}

- [Ingesting data by using the Spark ingestion UI](/docs/watsonxdata?topic=watsonxdata-ingest_spark_ui)
- [Ingesting data from local system](/docs/watsonxdata?topic=watsonxdata-ingest_spark_local)
- [Ingesting data from remote database](/docs/watsonxdata?topic=watsonxdata-ingest_spark_database)
- [Ingesting data from Delta Lake to Iceberg tables](/docs/watsonxdata?topic=watsonxdata-ingest_spark_deltalake)
- [Ingesting streaming data by using Spark Stream (Experimental)](/docs/watsonxdata?topic=watsonxdata-ingest_spark_stream)
