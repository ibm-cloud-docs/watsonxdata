---

copyright:
  years: 2022, 2026
lastupdated: "2026-05-11"

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

# Querying Databricks Unity Catalog using Spark engine
{: #data_stream_databricks2spark}

## About this task
{: #data_stream_databricks2spark1}

You can query remote Databricks Unity Catalog tables using the IBM® watsonx.data Spark engine through zero-copy data federation. This capability allows Spark to query both Delta Lake and Iceberg tables stored in Unity Catalog without requiring data movement or duplication.

This document demonstrates how to use the Unity Catalog Iceberg REST API endpoint (`/unity-catalog/iceberg-rest`) to query tables.

It first illustrates how to query a managed Iceberg table in Databricks that uses an external storage location, from {{site.data.keyword.lakehouse_short}} Spark. The examples cover both:

- Explicit storage credentials
- Vended credentials

The document then explains how to query a managed Delta table that uses Unity Catalog-managed (native) storage. This is achieved by reading the Delta table as an Iceberg table through the Iceberg REST API, using vended credentials.

For more information about Databricks Unity Catalog integration, see [Integrating Databricks Unity Catalog in {{site.data.keyword.lakehouse_short}}](/docs/watsonxdata?topic=watsonxdata-data_stream_databricks1).

## Before you begin
{: #data_stream_databricks2spark2}

Complete the prerequisites outlined in [Integrating Databricks Unity Catalog in {{site.data.keyword.lakehouse_short}}](/docs/watsonxdata?topic=watsonxdata-data_stream_databricks1), including:

- Databricks workspace with Unity Catalog enabled
- OAuth credentials or Personal Access Token
- Unity Catalog permissions configured
- Storage credentials (AWS S3, Azure, or GCS)
- Provisioned Spark engine (version 3.5 or later)

## Procedure
{: #data_stream_databricks2spark3}

1. Create a Spark session configuration with your Unity Catalog connection details to enable zero-copy querying.

   ```python
   from pyspark.sql import SparkSession

   WORKSPACE_URL = "https://<workspace-id>.cloud.databricks.com"
   UNITY_CATALOG_URL = f"{WORKSPACE_URL}/api/2.1/unity-catalog/iceberg-rest"
   CATALOG_NAME = "your_catalog_name"
   SCHEMA_NAME = "your_schema_name"
   TABLE_NAME = "your_table_name"
   OAUTH_CLIENT_ID = "your_oauth_client_id"
   OAUTH_CLIENT_SECRET = "your_oauth_client_secret"
   # Configure explicit storage credentials only when not using credential vending
   # AWS_ACCESS_KEY_ID = "your_aws_access_key"
   # AWS_SECRET_ACCESS_KEY = "your_aws_secret_key"

   spark = SparkSession.builder \
       .appName("Iceberg-REST-UC") \
       .config("spark.jars.packages",
           "org.apache.iceberg:iceberg-spark-runtime-3.5_2.12:1.5.0,"
           "org.apache.iceberg:iceberg-aws-bundle:1.5.0") \
       .config("spark.sql.extensions",
           "org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions") \
       .config(f"spark.sql.catalog.{CATALOG_NAME}",
           "org.apache.iceberg.spark.SparkCatalog") \
       .config(f"spark.sql.catalog.{CATALOG_NAME}.type", "rest") \
       .config(f"spark.sql.catalog.{CATALOG_NAME}.uri", UNITY_CATALOG_URL) \
       .config(f"spark.sql.catalog.{CATALOG_NAME}.warehouse", CATALOG_NAME) \
       .config(f"spark.sql.catalog.{CATALOG_NAME}.scope", "all-apis") \
       .config(f"spark.sql.catalog.{CATALOG_NAME}.rest.auth.type", "oauth2") \
       .config(f"spark.sql.catalog.{CATALOG_NAME}.oauth2-server-uri",
           f"{WORKSPACE_URL}/oidc/v1/token") \
       .config(f"spark.sql.catalog.{CATALOG_NAME}.credential",
           f"{OAUTH_CLIENT_ID}:{OAUTH_CLIENT_SECRET}") \

       # Use the following configurations to enable credential vending.
       # Do not configure explicit storage credentials when using this option.
       .config(f"spark.sql.catalog.{CATALOG_NAME}.header.X-Iceberg-Access-Delegation",
           "vended-credentials") \
       .config("spark.hadoop.fs.s3a.aws.credentials.provider",
           "org.apache.iceberg.aws.s3.S3V4RestSignerClient") \

       # Alternatively, configure explicit S3 credentials (disable the above settings if used).
       # .config("spark.hadoop.fs.s3a.access.key", AWS_ACCESS_KEY_ID) \
       # .config("spark.hadoop.fs.s3a.secret.key", AWS_SECRET_ACCESS_KEY) \

       .getOrCreate()
   ```
   {: codeblock}

   Replace placeholder values

   Update the following placeholders in the script below:

   - `<workspace-id>`: Your Databricks workspace identifier. Example workspace URLs:
     - `https://dbc-a1b2345c-d6e7.cloud.databricks.com/`
     - `https://adb-1234567890123456.7.azuredatabricks.net/`
   - `your_catalog_name`: Name of your Unity Catalog
   - `your_schema_name`: Name of your schema
   - `your_table_name`: Name of your table
   - `your_oauth_client_id`: OAuth client ID
   - `your_oauth_client_secret`: OAuth client secret

   If you plan to use explicit storage credentials, replace the following:

   - `your_aws_access_key`: AWS access key (for Amazon S3 storage)
   - `your_aws_secret_key`: AWS secret key (for Amazon S3 storage)

   The OAuth client ID and secret can be obtained from Service Principals in Databricks. For more information, see [Integrating Databricks Unity Catalog in {{site.data.keyword.lakehouse_short}}](/docs/watsonxdata?topic=watsonxdata-data_stream_databricks1).
   {: note}

2. Choose a submission method

   You can query remote Unity Catalog tables using one of three    methods:

   | Method | Best for | Documentation |
   | -------- | ---------- | --------------- |
   | SparkLab (VS Code) | Interactive development, testing, debugging | [VS Code Development Environment](/docs/watsonxdata?topic=watsonxdata-sparklabs) |
   | REST API | Automation, CI/CD pipelines, programmatic control | [Submitting Spark Application by using REST API](/docs/watsonxdata?topic=watsonxdata-spark-api) |
   | CPDCTL CLI | Command-line submissions, shell scripts, DevOps workflows | [Submitting Spark Application by using CPDCTL](/docs/watsonxdata?topic=watsonxdata-spark-cpdctl) |
   {: caption="Querying methods"}

3. Query remote Iceberg tables by using SparkLab

   1. Open SparkLab in {{site.data.keyword.lakehouse_short}}.
   2. Create a new PySpark script.
   3. Add the following code:

      ```python
      from pyspark.sql import SparkSession

      WORKSPACE_URL = "https://<workspace-id>.cloud.databricks.com"
      UNITY_CATALOG_URL = f"{WORKSPACE_URL}/api/2.1/unity-catalog/iceberg-rest"
      CATALOG_NAME = "your_catalog_name"
      SCHEMA_NAME = "your_schema_name"
      TABLE_NAME = "your_table_name"
      OAUTH_CLIENT_ID = "your_client_id"
      OAUTH_CLIENT_SECRET = "your_client_secret"
      # Configure explicit storage credentials only when not using credential vending
      # AWS_ACCESS_KEY_ID = "your_access_key"
      # AWS_SECRET_ACCESS_KEY = "your_secret_key"

      spark = SparkSession.builder \
          .appName("Iceberg-REST-UC") \
          .config("spark.jars.packages",
              "org.apache.iceberg:iceberg-spark-runtime-3.5_2.12:1.5.0,"
              "org.apache.iceberg:iceberg-aws-bundle:1.5.0") \
          .config("spark.sql.extensions",
              "org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions") \
          .config(f"spark.sql.catalog.{CATALOG_NAME}",
              "org.apache.iceberg.spark.SparkCatalog") \
          .config(f"spark.sql.catalog.{CATALOG_NAME}.type", "rest") \
          .config(f"spark.sql.catalog.{CATALOG_NAME}.uri", UNITY_CATALOG_URL) \
          .config(f"spark.sql.catalog.{CATALOG_NAME}.warehouse", CATALOG_NAME) \
          .config(f"spark.sql.catalog.{CATALOG_NAME}.scope", "all-apis") \
          .config(f"spark.sql.catalog.{CATALOG_NAME}.rest.auth.type", "oauth2") \
          .config(f"spark.sql.catalog.{CATALOG_NAME}.oauth2-server-uri",
              f"{WORKSPACE_URL}/oidc/v1/token") \
          .config(f"spark.sql.catalog.{CATALOG_NAME}.credential",
              f"{OAUTH_CLIENT_ID}:{OAUTH_CLIENT_SECRET}") \

          # Use the following configurations to enable credential vending.
          # Do not configure explicit storage credentials when using this option.
          .config(f"spark.sql.catalog.{CATALOG_NAME}.header.X-Iceberg-Access-Delegation",
              "vended-credentials") \
          .config("spark.hadoop.fs.s3a.aws.credentials.provider",
              "org.apache.iceberg.aws.s3.S3V4RestSignerClient") \

          # Alternatively, configure explicit S3 credentials (disable the above settings if used).
          # .config("spark.hadoop.fs.s3a.access.key", AWS_ACCESS_KEY_ID) \
          # .config("spark.hadoop.fs.s3a.secret.key", AWS_SECRET_ACCESS_KEY) \

          .getOrCreate()

      print(f"Namespaces in catalog: {CATALOG_NAME}")
      spark.sql(f"SHOW NAMESPACES IN {CATALOG_NAME}").show(truncate=False)

      print(f"Tables in namespace: {CATALOG_NAME}.{SCHEMA_NAME}")
      spark.sql(f"SHOW TABLES IN {CATALOG_NAME}.{SCHEMA_NAME}").show(truncate=False)

      spark.sql(f"DESCRIBE EXTENDED {CATALOG_NAME}.{SCHEMA_NAME}.{TABLE_NAME}").show(truncate=False)

      full_table_name = f"{CATALOG_NAME}.{SCHEMA_NAME}.{TABLE_NAME}"
      print(f"Querying: {full_table_name}")

      df = spark.sql(f"SELECT * FROM {full_table_name}")
      df.printSchema()
      df.show(20, truncate=False)

      count = df.count()
      print(f"Total records: {count}")

      spark.stop()
      ```
      {: codeblock}

4. Run the script.

5. Query managed Delta tables with Unity Catalog-managed storage.

   You can query managed Delta tables that use Unity Catalog-managed (native) storage from {{site.data.keyword.lakehouse_short}} Spark by reading them as Iceberg tables through the Iceberg REST API.

   1. To enable this capability, you must first configure the Delta table in Databricks to support the Uniform format.

      Ensure that you have the required permissions to modify table properties and run maintenance operations on the target table in Databricks.
      {: note}

   2. Run the following commands in the Databricks SQL Editor:

      ```sql
      ALTER TABLE spark_deegandh.test_schema.sensor_readings
      SET TBLPROPERTIES (
        'delta.enableDeletionVectors' = 'false'
      );

      REORG TABLE spark_deegandh.test_schema.sensor_readings APPLY (PURGE);

      ALTER TABLE spark_deegandh.test_schema.sensor_readings
      SET TBLPROPERTIES (
        'delta.enableIcebergCompatV2' = 'true',
        'delta.columnMapping.mode' = 'name',
        'delta.universalFormat.enabledFormats' = 'iceberg'
      );

      SHOW TBLPROPERTIES spark_deegandh.test_schema.sensor_readings;
      ```
      {: codeblock}


   After completing these steps, the Delta table is enabled for Uniform and can be accessed as an Iceberg table through the Unity Catalog Iceberg REST API.

   You should see the following properties in the output:

   - `delta.universalFormat.enabledFormats = iceberg`
   - `delta.enableIcebergCompatV2 = true`

   3. You can then query the Delta table from {{site.data.keyword.lakehouse_short}} Spark by using the same script, leveraging credential vending through the Unity Catalog Iceberg REST API endpoint (`/unity-catalog/iceberg-rest`), as described in the previous step.

      Deletion vectors must be disabled and fully purged before enabling Iceberg compatibility. If this step is skipped, the configuration will fail.
      {: note}

      For more details about Uniform and creating Delta tables with Uniform (universal format) enabled, see the official Databricks documentation: [Delta Uniform: Universal Format for Lakehouse Interoperability](https://docs.databricks.com/en/delta/uniform.html).

## Results
{: #data_stream_databricks2spark4}

You can now query remote data from Databricks Unity Catalog without copying data. The queries execute directly against the data in the external storage location.

## Example output for Iceberg table
{: #data_stream_databricks2spark5}

Namespaces in catalog: `spark_deegandh`

   ```sql
   +---------------------------+
   |namespace                  |
   +---------------------------+
   |default                    |
   |delta_share_demo           |
   |feb14schema                |
   |information_schema         |
   |mrmadira_external_schema   |
   +---------------------------+
   ```
   {: screen}

Tables in namespace: `spark_deegandh.feb14schema`:

   ```sql
   +-----------+--------------------+-----------+
   |namespace  |tableName           |isTemporary|
   +-----------+--------------------+-----------+
   |feb14schema|avengers            |false      |
   |feb14schema|cims_test_result    |false      |
   |feb14schema|iceberg_orders      |false      |
   |feb14schema|mrmadira_csv_table  |false      |
   +-----------+--------------------+-----------+
   ```
   {: screen}

Querying: `spark_deegandh.feb14schema.iceberg_orders`:

Schema:

   ```sql
   root
    |-- order_id: long (nullable = true)
    |-- customer_id: long (nullable = true)
    |-- order_ts: timestamp (nullable = true)
    |-- total_amt: decimal(12,2) (nullable = true)
   ```
   {: screen}

Data (first 20 rows):

   ```sql
   +--------+-----------+-------------------+---------+
   |order_id|customer_id|order_ts           |total_amt|
   +--------+-----------+-------------------+---------+
   |22222   |22222      |2022-01-01 00:00:00|100.00   |
   +--------+-----------+-------------------+---------+
   ```
   {: screen}

   Total records: 1

## Example output for the Delta table
{: #data_stream_databricks2spark6}

Query:

   ```python
   spark.sql(f"SHOW NAMESPACES IN {CATALOG_NAME}").show(truncate=False)
   ```
   {: codeblock}

Output:

Namespaces in catalog: `spark_deegandh`

   ```sql
   +----------------------------------+
   |namespace                         |
   +----------------------------------+
   |default                           |
   |delta_share_demo                  |
   |feb14schema                       |
   |information_schema                |
   |mrmadira_external_schema          |
   |test_schema                       |
   |tpcdsdbiceberg_10tb_partitioned_uc|
   +----------------------------------+
   ```
   {: screen}

Query:

   ```python
   spark.sql(f"SHOW TABLES IN {CATALOG_NAME}.{SCHEMA_NAME}").show(truncate=False)
   ```
   {: codeblock}

Output:

   Tables in namespace: `spark_deegandh.test_schema`:

   ```sql
   +-----------+---------------+-----------+
   |namespace  |tableName      |isTemporary|
   +-----------+---------------+-----------+
   |test_schema|sensor_readings|false      |
   +-----------+---------------+-----------+
   ```
   {: screen}

Query:

   ```python
   df = spark.sql(f"SELECT * FROM {full_table_name}")

   df.printSchema()

   df.show(20, truncate=False)

   count = df.count()

   print(f"Total records: {count}")
   ```
   {: codeblock}

Output:

Querying: `spark_deegandh.test_schema.sensor_readings`:

Schema:

   ```sql
   root
    |-- sensor_id: integer (nullable = true)
    |-- location: string (nullable = true)
    |-- temperature: double (nullable = true)
    |-- humidity: double (nullable = true)
    |-- battery_level: double (nullable = true)
    |-- reading_timestamp: string (nullable = true)
    |-- is_active: boolean (nullable = true)
   ```
   {: screen}

Data (first 20 rows):

   ```sql
   +---------+-----------+-----------+--------+-------------+-------------------+---------+
   |sensor_id|location   |temperature|humidity|battery_level|reading_timestamp  |is_active|
   +---------+-----------+-----------+--------+-------------+-------------------+---------+
   |1001     |Warehouse-A|24.5       |60.2    |89.5         |2026-04-01 10:00:00|true     |
   |1002     |Warehouse-B|26.1       |58.0    |76.3         |2026-04-01 10:05:00|true     |
   |1003     |Warehouse-C|22.8       |65.4    |54.2         |2026-04-01 10:10:00|false    |
   |1004     |Warehouse-A|25.0       |61.5    |88.0         |2026-04-01 10:15:00|true     |
   |1005     |Warehouse-B|27.3       |55.2    |70.1         |2026-04-01 10:20:00|true     |
   |1006     |Warehouse-C|23.5       |66.8    |49.9         |2026-04-01 10:25:00|false    |
   |1007     |Warehouse-A|24.8       |62.1    |85.7         |2026-04-01 10:30:00|true     |
   |1008     |Warehouse-B|26.9       |57.6    |72.4         |2026-04-01 10:35:00|true     |
   |1009     |Warehouse-C|22.2       |67.0    |45.3         |2026-04-01 10:40:00|false    |
   |1010     |Warehouse-A|25.3       |60.9    |87.2         |2026-04-01 10:45:00|true     |
   +---------+-----------+-----------+--------+-------------+-------------------+---------+
   ```
   {: screen}

Total records: `10`

## Related information
{: #data_stream_databricks2spark6}

- [Integrating Databricks Unity Catalog in {{site.data.keyword.lakehouse_short}}](/docs/watsonxdata?topic=watsonxdata-data_stream_databricks1)
- [Databricks Unity Catalog documentation](https://docs.databricks.com/data-governance/unity-catalog/index.html)
- [Unity Catalog privileges and securable objects](https://docs.databricks.com/data-governance/unity-catalog/manage-privileges/privileges.html)
- [Delta UniForm: Universal Format for Lakehouse Interoperability](https://docs.databricks.com/en/delta/uniform.html)
