---

copyright:
  years: 2022, 2026
lastupdated: "2026-04-08"

keywords: lakehouse, remote data, confluent, {{site.data.keyword.lakehouse_short}}

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

# Querying Databricks Iceberg tables using Presto engine
{: #data_stream_databricks3presto}

## About this task
{: #data_stream_databricks3presto1}

You can query remote Databricks Iceberg tables using the {{site.data.keyword.lakehouse_full}} Presto engine by registering Databricks as a custom data source for zero-copy data federation.

- Presto connects to Databricks through the Iceberg REST Catalog API interface, not Unity Catalog API directly.
- Presto does not currently support vended-credentials for Databricks integration.
- You must configure explicit storage credentials (AWS S3 and Azure Data Lake Storage Gen2) to access the underlying data files.
- Presto supports Iceberg tables only; Delta Lake tables are not supported.
- For general information about Databricks Unity Catalog integration, see [Integrating Databricks Unity Catalog in {{site.data.keyword.lakehouse_short}}](/docs/watsonxdata?topic=watsonxdata-data_stream_databricks1).

## Before you begin
{: #data_stream_databricks3presto2}

Complete the prerequisites outlined in [Integrating Databricks Unity Catalog in {{site.data.keyword.lakehouse_short}}](/docs/watsonxdata?topic=watsonxdata-data_stream_databricks1), including:

- Databricks workspace with Unity Catalog enabled
- Iceberg tables created in Databricks Unity Catalog
- Personal Access Token with `unity-catalog` API scope
- **Workspace URL:** `https://<workspace-instance>.cloud.databricks.com`
- Unity Catalog permissions configured
- Provisioned Presto engine in {{site.data.keyword.lakehouse_short}}
- **Iceberg REST Catalog endpoint:** `https://<workspace-instance>.cloud.databricks.com/api/2.1/unity-catalog/iceberg-rest`
- **Catalog name:** Name of the Unity Catalog containing Iceberg tables
- Access credentials for the external storage location (AWS S3 or Azure)

Use of vended credentials is currently not supported. Hence, Presto requires explicit storage credentials.
{: note}


## Procedure
{: #data_stream_databricks3presto3}

1. Register Databricks as a custom data source

   1. In the {{site.data.keyword.lakehouse_short}} console, click **Infrastructure manager**.
   2. Click **Add component > Add data source**.
   3. Select **Custom** as the data source type.
   4. Enter a display name (e.g., `databricks_iceberg`).
   5. In the **Properties** section, add the following properties:

      **For AWS S3:**

      ```properties
      connector.name=iceberg
      iceberg.catalog.type=rest
      iceberg.rest.uri=https://<workspace-instance>.cloud.databricks.com/api/2.1/unity-catalog/iceberg-rest
      iceberg.rest.auth.type=OAUTH2
      iceberg.rest.auth.oauth2.token=<databricks-access-token>
      iceberg.catalog.warehouse=<catalog-name>
      hive.s3.aws-access-key=<aws-access-key>
      hive.s3.aws-secret-key=<aws-secret-key>
      ```
      {: codeblock}

      **For Azure Data Lake Storage Gen2:**

      ```properties
      connector.name=iceberg
      iceberg.catalog.type=rest
      iceberg.rest.uri=https://<workspace-url>/api/2.1/unity-catalog/iceberg-rest
      iceberg.rest.auth.type=OAUTH2
      iceberg.rest.auth.oauth2.token=<databricks-access-token>
      iceberg.catalog.warehouse=<catalog-name>
      hive.azure.abfs-storage-account=<storage-account-name>
      hive.azure.abfs-access-key=<storage-account-key>
      ```
      {: codeblock}

      Replace the placeholders in the 2 storage properties as follows:
      - `<workspace-url>`: Your Databricks workspace URL
      - `<databricks-access-token>`: Your Databricks personal access token
      - `<catalog-name>`: The Unity Catalog name containing your Iceberg tables
      - Storage credential placeholders with your actual credentials

   6. Click **Create**.

2. Create a catalog for the data source

   1. Click **Data manager > Catalogs**.
   2. Click **Create catalog**.
   3. Select **Iceberg** as the catalog type.
   4. Enter a catalog name (e.g., `databricks_catalog`).
   5. In the **Data source** field, select the custom data source you created (`databricks_iceberg`).
   6. Click **Create**.

3. Associate the catalog with Presto engine

   1. Click **Infrastructure manager**.
   2. Select your Presto engine from the list.
   3. Click **Associate catalog**.
   4. Select the catalog you created (`databricks_catalog`).
   5. Click **Associate**.

4. Query Databricks Iceberg tables

   1. Click **Query workspace**.
   2. Select your Presto engine from the engine dropdown.
   3. Run queries against your remote Databricks Iceberg tables using fully qualified table names:

      ```sql
      -- List available schemas (namespaces)
      SHOW SCHEMAS IN databricks_catalog;

      -- List tables in a schema
      SHOW TABLES IN databricks_catalog.<schema_name>;

      -- Describe table structure
      DESCRIBE databricks_catalog.<schema_name>.<table_name>;

      -- Query data
      SELECT * FROM databricks_catalog.<schema_name>.<table_name> LIMIT 10;

      -- Get row count
      SELECT COUNT(*) FROM databricks_catalog.<schema_name>.<table_name>;

      -- Filter and aggregate
      SELECT
          column1,
          COUNT(*) as count,
          AVG(column2) as avg_value
      FROM databricks_catalog.<schema_name>.<table_name>
      WHERE column3 > 100
      GROUP BY column1
      ORDER BY count DESC;
      ```
      {: codeblock}

## Results
{: #data_stream_databricks3presto4}

You can now query Iceberg tables from Databricks Unity Catalog using Presto. The queries execute directly on the data in the external storage location without copying data into {{site.data.keyword.lakehouse_short}}.

## Example queries and outputs
{: #data_stream_databricks3presto5}

List schemas in a catalog:

   ```sql
   SHOW SCHEMAS IN databricks_catalog;
   ```
   {: codeblock}

Output:

   ```sql
   Schema
   --------------------------
   default
   delta_share_demo
   feb14schema
   information_schema
   mrmadira_external_schema
   tpcdsdbiceberg_10tb_partitioned_uc
   ```
   {: screen}

List tables in a schema:

   ```sql
   SHOW TABLES IN databricks_catalog.feb14schema;
   ```
   {: codeblock}

Output:

   ```sql
   Table
   -----------------
   avengers
   cims_test_result
   iceberg_orders
   mrmadira_csv_table
   ```
   {: screen}

Describe table structure:

   ```sql
   DESCRIBE databricks_catalog.feb14schema.iceberg_orders;
   ```
   {: codeblock}

Output:

   ```sql
   Column       | Type                  | Extra | Comment
   -------------|-----------------------|-------|--------
   order_id     | bigint               |       |
   customer_id  | bigint               |       |
   order_ts     | timestamp(6)         |       |
   total_amt    | decimal(12,2)        |       |
   ```
   {: screen}

Query a table:

   ```sql
   SELECT * FROM databricks_catalog.feb14schema.iceberg_orders LIMIT 10;
   ```
   {: codeblock}

Output:

   ```sql
   order_id | customer_id | order_ts            | total_amt
   ---------|-------------|---------------------|----------
   22222    | 22222       | 2022-01-01 00:00:00 | 100.00
   ```
   {: screen}

## Related information
{: #data_stream_databricks3presto6}

- [Integrating Databricks Unity Catalog in {{site.data.keyword.lakehouse_short}}](/docs/watsonxdata?topic=watsonxdata-data_stream_databricks1)
- [Databricks Unity Catalog documentation](https://docs.databricks.com/data-governance/unity-catalog/index.html)
- [Unity Catalog privileges and securable objects](https://docs.databricks.com/data-governance/unity-catalog/manage-privileges/privileges.html)
