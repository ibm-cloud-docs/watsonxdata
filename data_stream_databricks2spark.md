---

copyright:
  years: 2022, 2026
lastupdated: "2026-04-02"

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

You can query remote Databricks Unity Catalog tables using the {{site.data.keyword.lakehouse_full}} Spark engine through zero-copy data federation. Spark supports querying both Delta Lake and Iceberg tables stored in Databricks Unity Catalog without copying data.

For general information about Databricks Unity Catalog integration, see [Integrating Databricks Unity Catalog in {{site.data.keyword.lakehouse_short}}](/docs/watsonxdata?topic=watsonxdata-data_stream_databricks1).

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

   **Basic configuration with OAuth authentication:**

   ```python
   from pyspark.sql import SparkSession

   WORKSPACE_URL = "https://<workspace-id>.cloud.databricks.com"
   UNITY_CATALOG_URL = f"{WORKSPACE_URL}/api/2.1/unity-catalog/iceberg-rest"
   CATALOG_NAME = "your_catalog_name"
   OAUTH_CLIENT_ID = "your_oauth_client_id"
   OAUTH_CLIENT_SECRET = "your_oauth_client_secret"
   AWS_ACCESS_KEY_ID = "your_aws_access_key"
   AWS_SECRET_ACCESS_KEY = "your_aws_secret_key"
   S3_REGION = "your_s3_region"

   spark = SparkSession.builder \
       .appName("Query-Databricks-Unity-Catalog") \
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
       .config("spark.hadoop.fs.s3a.access.key", AWS_ACCESS_KEY_ID) \
       .config("spark.hadoop.fs.s3a.secret.key", AWS_SECRET_ACCESS_KEY) \
       .config("spark.hadoop.fs.s3a.endpoint", f"s3.{S3_REGION}.amazonaws.com") \
       .getOrCreate()
   ```
   {: codeblock}

   Replace the following placeholders:

   - `<workspace-id>`: Your Databricks workspace identifier
   - `your_catalog_name`: Your Unity Catalog name
   - `your_oauth_client_id`: OAuth Client ID
   - `your_oauth_client_secret`: OAuth Client Secret
   - `your_aws_access_key`: AWS access key (for S3 storage)
   - `your_aws_secret_key`: AWS secret key (for S3 storage)
   - `your_s3_region`: Your S3 region

   The catalog name in the configuration is a local alias. You can use any name, but it must match the catalog name used in SQL queries.
   {: note}

2. Choose a submission method

   You can query remote Unity Catalog tables using one of three    methods:

   | Method | Best for | Documentation |
   | -------- | ---------- | --------------- |
   | SparkLab (VS Code) | Interactive development, testing, debugging | [VS Code Development Environment](/docs/watsonxdata?topic=watsonxdata-sparklabs) |
   | REST API | Automation, CI/CD pipelines, programmatic control | [Submitting Spark Application by using REST API](/docs/watsonxdata?topic=watsonxdata-spark-api) |
   | CPDCTL CLI | Command-line submissions, shell scripts, DevOps workflows | [Submitting Spark Application by using CPDCTL](/docs/watsonxdata?topic=watsonxdata-spark-cpdctl) |
   {: caption="Querying methods"}

3. Query remote Unity Catalog tables

   **Using SparkLab:**

   1. Open SparkLab in {{site.data.keyword.lakehouse_short}}.
   2. Create a new PySpark script.
   3. Add the following code:

      ```python
      from pyspark.sql import SparkSession

      WORKSPACE_URL = "https://<workspace-id>.cloud.databricks.com"
      UNITY_CATALOG_URL = f"{WORKSPACE_URL}/api/2.1/unity-catalog/iceberg-rest"
      CATALOG_NAME = "spark_deegandh"
      SCHEMA_NAME = "feb14schema"
      TABLE_NAME = "iceberg_orders"
      OAUTH_CLIENT_ID = "your_client_id"
      OAUTH_CLIENT_SECRET = "your_client_secret"
      AWS_ACCESS_KEY_ID = "your_access_key"
      AWS_SECRET_ACCESS_KEY = "your_secret_key"
      S3_REGION = "us-west-2"

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
          .config(f"spark.sql.catalog.{CATALOG_NAME}. warehouse", CATALOG_NAME) \
          .config(f"spark.sql.catalog.{CATALOG_NAME}.scope", "all-apis") \
          .config(f"spark.sql.catalog.{CATALOG_NAME}.rest.auth.type", "oauth2") \
          .config(f"spark.sql.catalog.{CATALOG_NAME}.oauth2-server-uri",
              f"{WORKSPACE_URL}/oidc/v1/token") \
          .config(f"spark.sql.catalog.{CATALOG_NAME}.credential",
              f"{OAUTH_CLIENT_ID}:{OAUTH_CLIENT_SECRET}") \
          .config("spark.hadoop.fs.s3a.access.key", AWS_ACCESS_KEY_ID) \
          .config("spark.hadoop.fs.s3a.secret.key", AWS_SECRET_ACCESS_KEY) \
          .config("spark.hadoop.fs.s3a.endpoint", f"s3.{S3_REGION}.amazonaws.com") \
          .getOrCreate()

      print(f"Namespaces in catalog: {CATALOG_NAME}")
      spark.sql(f"SHOW NAMESPACES IN {CATALOG_NAME}").show(truncate=False)

      print(f"Tables in namespace: {CATALOG_NAME}.{SCHEMA_NAME}")
      spark.sql(f"SHOW TABLES IN {CATALOG_NAME}.{SCHEMA_NAME}").show(truncate=False)

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

## Results
{: #data_stream_databricks2spark4}

You can now query remote data from Databricks Unity Catalog without copying data. The queries execute directly against the data in the external storage location.

## Example output
{: #data_stream_databricks2spark5}

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

## Related information
{: #data_stream_databricks2spark6}

- [Integrating Databricks Unity Catalog in {{site.data.keyword.lakehouse_short}}](/docs/watsonxdata?topic=watsonxdata-data_stream_databricks1)
- [Databricks Unity Catalog documentation](https://docs.databricks.com/data-governance/unity-catalog/index.html)
- [Unity Catalog privileges and securable objects](https://docs.databricks.com/data-governance/unity-catalog/manage-privileges/privileges.html)
