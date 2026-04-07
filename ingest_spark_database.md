---

copyright:
  years: 2022, 2025
lastupdated: "2026-04-07"

keywords: watsonx.data, data ingestion, source file

subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Ingesting data from databases
{: #ingest_spark_database}

You can ingest data from connected databases into {{site.data.keyword.lakehouse_full}} by using the Spark ingestion UI. This flow enables you to browse and select tables from your connected database and ingest them into your data lakehouse.

## Before you begin
{: #ingest_spark_database1}

- Review the [prerequisites](/docs/watsonxdata?topic=watsonxdata-ingest_spark_ui#ingest_spark_ui3) for using the Spark ingestion UI.
- The database must be connected to {{site.data.keyword.lakehouse_short}} before it appears in the list. Contact your administrator if the database you need is not available.
- To ensure the ingestion is accurate and consistent with source data, all input schemas must be identical or compatible with the target table schema.

## Procedure
{: #ingest_spark_database2}

1. Log in to the {{site.data.keyword.lakehouse_short}} console.
2. From the navigation menu, select **Data manager**.
3. Click **Ingest data**.
4. Select **Databases** as the ingestion flow.
5. From the **Select database** dropdown, choose the connected database you want to ingest from.
6. If you need to add a new database connection, click **Add** next to the database selector.
7. After selecting a database, the available schemas are displayed in the **Schemas** panel.
8. In the **Database** panel on the left:
   - The **Schemas** section displays the number of schemas available
   - Use the **Find schema** search box to filter schemas by name
   - If no schemas are displayed, the message "No schemas in this database" appears with guidance to try selecting a different database
9. In the **Browse Table** panel in the center:
   - After selecting a schema, the **Selected table** and **Schema** information is displayed at the top
   - Use the **Find table** search box to filter tables by name
   - When no schema is selected, the message "No schema selected" appears with guidance: "Files within the selected schema will appear here. Try selecting a schema."
10. Select the tables you want to ingest by clicking on them.
17. See [Configuring target table settings](/docs/watsonxdata?topic=watsonxdata-ingest_spark_ui#ingest_spark_ui6) in the parent topic.
18. See [Configuring job details](/docs/watsonxdata?topic=watsonxdata-ingest_spark_ui#ingest_spark_ui7) in the parent topic.
5. Click **Done** to submit the ingestion job, or **Cancel** to discard the configuration.

## Results
{: #ingest_spark_database3}

After the ingestion job completes successfully, the data from the source database tables is loaded into the target table in {{site.data.keyword.lakehouse_short}}. The source database tables remain unchanged.

## Related information
{: #ingest_spark_database4}

- [Ingesting data by using the Spark ingestion UI](/docs/watsonxdata?topic=watsonxdata-ingest_spark_ui)
- [Ingesting data from local system](/docs/watsonxdata?topic=watsonxdata-ingest_spark_local)
- [Ingesting data from remote storage](/docs/watsonxdata?topic=watsonxdata-ingest_spark_storage)
- [Ingesting data from Delta Lake to Iceberg tables](/docs/watsonxdata?topic=watsonxdata-ingest_spark_deltalake)
- [Ingesting streaming data by using Spark Stream (Experimental)](/docs/watsonxdata?topic=watsonxdata-ingest_spark_stream)
