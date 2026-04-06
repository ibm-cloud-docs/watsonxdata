---

copyright:
  years: 2022, 2025
lastupdated: "2026-04-06"

keywords: {{site.data.keyword.lakehouse_short}}, data ingestion, source file

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

# Migrating data from Delta Lake to Iceberg tables
{: #ingest_spark_deltalake}

You can migrate data from Delta Lake tables to Iceberg tables in {{site.data.keyword.lakehouse_full}} by using the Spark ingestion UI. This flow enables you to select source Delta Lake tables, map them to target Iceberg tables, and configure migration jobs.

## Before you begin
{: #ingest_spark_deltalake1}

- Review the [prerequisites](/docs/watsonxdata?topic=watsonxdata-ingest_spark_ui#ingest_spark_ui3) for using the Spark ingestion UI.
- The Delta Lake storage must be registered in {{site.data.keyword.lakehouse_short}}. Contact your administrator if the storage you need is not available.

## Procedure
{: #ingest_spark_deltalake2}

1. Log in to the {{site.data.keyword.lakehouse_short}} console.
2. From the navigation menu, select **Data manager**.
3. Click **Ingest data**.
4. Select **Delta Lake to Iceberg table migrations** as the ingestion flow.
5. In the **Source Delta Lake tables** section:
   1. **Migration settings**: Select the snapshot option:
      - **Latest snapshot only** (default): Migrate only the current version of the Delta Lake table
      - **All snapshots (full history)**: Migrate the complete history of the Delta Lake table, preserving all versions

   2. **Select storage**: Choose the storage location containing the Delta Lake tables from the dropdown (e.g., "bucketcos").

   3. **All tables**: The section displays the number of available tables (e.g., "All tables (1)").
      - Below this, you'll see the message: "Select tables to map to target catalog"

   4. **Search tables**: Use the search box to filter tables by name.

   5. **Select tables**: Click the checkbox next to each table you want to migrate (e.g., "new/test1").

6. In the **Target Iceberg table** section:

   1. **Select Catalog**: Choose the target catalog from the dropdown (e.g., "shibil_catalog").

   2. **Table selection status**: The section displays "0 tables selected" until you select source tables.
      - After selecting source tables, the message changes to: "Select tables to begin mapping to target"
      - Additional guidance: "Selected tables will appear here. Please select tables from the source panel."

   3. After selecting source tables, the mapping interface allows you to map each source Delta Lake table to a target Iceberg table.

7. In the **Job details** section:

   1. **Job ID**: A unique job identifier is automatically generated (e.g., "migration-1774936072150").

   2. **Select engine**: Choose the Spark engine to use for the migration job from the dropdown (default: "(Spark) Spark").

   3. **Configuration**: Expand this section to configure additional settings:

      - **API key**: Enter an API key if required for authentication.

      - **Table property**: Specify table properties in key-value format. Use comma-separated key-value pairs.
        - Example: `key1=value1, key2=value2`
        - Common properties include compression settings, partitioning options, and table metadata

      - **Number of parallel migrations**: Specify how many tables to migrate in parallel (default: 1).
        - Use the minus (-) and plus (+) buttons to adjust the value
        - Higher values can speed up migration but consume more resources

4. Click **Done** to submit the migration job, or **Cancel** to discard the configuration.

## Results
{: #ingest_spark_deltalake3}

After the migration job completes successfully:

- The Delta Lake tables are converted to Iceberg format in the target catalog.
- The source Delta Lake tables remain unchanged in the original storage location.
- If "All snapshots (full history)" was selected, the complete version history is preserved in the Iceberg table.

## Related information
{: #ingest_spark_deltalake4}

- [Ingesting data by using the Spark ingestion UI](/docs/watsonxdata?topic=watsonxdata-ingest_spark_ui)
- [Ingesting data from local system](/docs/watsonxdata?topic=watsonxdata-ingest_spark_local)
- [Ingesting data from remote storage](/docs/watsonxdata?topic=watsonxdata-ingest_spark_storage)
- [Ingesting data from remote database](/docs/watsonxdata?topic=watsonxdata-ingest_spark_database)
- [Ingesting streaming data by using Spark Stream (Experimental)](/docs/watsonxdata?topic=watsonxdata-ingest_spark_stream)
