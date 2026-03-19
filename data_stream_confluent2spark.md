---

copyright:
  years: 2022, 2026
lastupdated: "2026-03-19"

keywords: lakehouse, data streaming, confluent, {{site.data.keyword.lakehouse_short}}

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

# Querying Confluent Tableflow using Spark engine
{: #data_stream_confluent2spark}

## About this task
{: #data_stream_confluent2spark_1}

You can query remote Confluent Tableflow tables using the {{site.data.keyword.lakehouse_full}} Spark engine through zero-copy data federation. Spark supports both Confluent Managed Storage and provider-integrated storage options.

## Before you begin
{: #data_stream_confluent2spark_2}

**Confluent requirements:**
- Active Confluent Cloud account
- Kafka cluster with Tableflow-enabled topics
- Tableflow API key and secret
- REST Catalog endpoint

   To obtain credentials:
   1. Log in to Confluent Cloud
   2. Navigate to your Tableflow-enabled topic
   3. Create a new API key and note the key and secret
   4. Copy the REST Catalog endpoint (format: `https://tableflow.{region}.aws.confluent.cloud/iceberg/catalog/organizations/{org-id}/environments/{env-id}`)

**{{site.data.keyword.lakehouse_short}} requirements:**
- Provisioned Spark engine
- Network connectivity to Confluent Cloud endpoint

**Storage-specific requirements:**
- **Confluent Managed Storage**: No additional requirements
- **Customer integration (AWS S3)**:
   - S3 bucket in the same region as your Kafka cluster
   - S3 access key and secret key

## Procedure
{: #data_stream_confluent2spark_3}

1. Configure Spark catalog properties for remote lakehouse access.

   Create a configuration dictionary with your Tableflow connection details to enable zero-copy querying.

   **For Confluent managed storage:**

   ```python
   tableflow_config = {
       "spark.sql.catalog.tableflow": "org.apache.iceberg.spark.SparkCatalog",
       "spark.sql.catalog.tableflow.type": "rest",
       "spark.sql.catalog.tableflow.uri": "https://tableflow.{CLOUD_REGION}.aws.confluent.cloud/iceberg/catalog/organizations/{ORG_ID}/environments/   {ENV_ID}",
       "spark.sql.catalog.tableflow.credential": "{APIKEY}:{SECRET}",
       "spark.sql.catalog.tableflow.io-impl": "org.apache.iceberg.aws.s3.S3FileIO",
       "spark.sql.catalog.tableflow.rest-metrics-reporting-enabled": "false",
       "spark.sql.catalog.tableflow.s3.remote-signing-enabled": "true",
       "spark.sql.catalog.tableflow.client.region": "{CLOUD_REGION}"
   }
   ```

   **For Customer integration (AWS S3):**

   Add these additional properties:

   ```python
   "spark.sql.catalog.tableflow.s3.access-key-id": "{S3_ACCESS_KEY}",
   "spark.sql.catalog.tableflow.s3.secret-access-key": "{S3_SECRET_KEY}",
   "spark.sql.catalog.tableflow.s3.region": "{S3_REGION}"
   ```

   Replace the placeholders:

   - `{CLOUD_REGION}`: Your Confluent cluster region (e.g., `us-east-1`)
   - `{ORG_ID}`: Your Confluent organization ID
   - `{ENV_ID}`: Your Confluent environment ID
   - `{APIKEY}:{SECRET}`: Your Tableflow API credentials
   - `{S3_ACCESS_KEY}`, `{S3_SECRET_KEY}`, `{S3_REGION}`: Your S3 credentials (for provider integration only)

   The catalog name `tableflow` is a local alias. You can use any name.
   {: note}

2. Choose a submission method

   You can query remote TableFlow tables using one of three methods:

   | Method | Best for | Documentation |
   | -------- | ---------- | --------------- |
   | SparkLab (VS Code) | Interactive development, testing, debugging | [VS Code Development Environment](/docs/watsonxdata?topic=watsonxdata-sparklabs) |
   | REST API | Automation, CI/CD pipelines, programmatic control | [Submitting Spark Application by using REST API](/docs/watsonxdata?topic=watsonxdata-spark-api) |
   | CPDCTL CLI | Command-line submissions, shell scripts, DevOps workflows | [Submitting Spark Application by using CPDCTL](/docs/watsonxdata?topic=watsonxdata-spark-cpdctl) |
   {: caption="Querying methods"}

3. Query remote Tableflow tables

   **Using SparkLab:**

   1. Open SparkLab in {{site.data.keyword.lakehouse_short}}.
   2. Create a new PySpark notebook.
   3. Add the following code:

   ```python
   from pyspark.sql import SparkSession

   # Create Spark session with TableFlow configuration
   spark = (
       SparkSession.builder
       .appName("Query Confluent TableFlow")
       .config("spark.sql.catalog.tableflow", "org.apache.iceberg.spark.SparkCatalog")
       .config("spark.sql.catalog.tableflow.type", "rest")
       .config("spark.sql.catalog.tableflow.uri", "https://tableflow.us-east-1.aws.confluent.cloud/iceberg/catalog/organizations/abc123/environments/   env-xyz")
       .config("spark.sql.catalog.tableflow.credential", "your-api-key:your-secret")
       .config("spark.sql.catalog.tableflow.io-impl", "org.apache.iceberg.aws.s3.S3FileIO")
       .config("spark.sql.catalog.tableflow.s3.remote-signing-enabled", "true")
       .config("spark.sql.catalog.tableflow.client.region", "us-east-1")
       .getOrCreate()
   )

   # Discover available namespaces (Kafka cluster IDs)
   print("Available namespaces:")
   spark.sql("SHOW NAMESPACES IN tableflow").show()

   # List tables in a namespace
   namespace = "lkc-xxxxx"  # Replace with your cluster ID
   print(f"Tables in {namespace}:")
   spark.sql(f"SHOW TABLES IN tableflow.`{namespace}`").show()

   # Query a table
   table_name = "your_topic_name"
   df = spark.sql(f"SELECT * FROM tableflow.`{namespace}`.{table_name} LIMIT 10")
   df.show()

   # Get row count
   count = spark.sql(f"SELECT COUNT(*) as count FROM tableflow.`{namespace}`.{table_name}").collect()[0]['count']
   print(f"Total rows: {count}")
   ```

4. Run the notebook.

   **Using REST API:**

   1. Create a PySpark script file (e.g., `query_tableflow.py`)
   2. Submit the application:

   ```bash
   curl -X POST "https://{wxd-host}/lakehouse/api/v2/spark_engines/{engine_id}/applications" \
     -H "Authorization: Bearer {token}" \
     -H "Content-Type: application/json" \
     -d '{
       "application_details": {
         "application": "s3://bucket/query_tableflow.py",
         "conf": {
           "spark.sql.catalog.tableflow": "org.apache.iceberg.spark.SparkCatalog",
           "spark.sql.catalog.tableflow.type": "rest",
           "spark.sql.catalog.tableflow.uri": "https://tableflow.us-east-1.aws.confluent.cloud/iceberg/catalog/organizations/{ORG_ID}/environments/{ENV_ID}   ",
           "spark.sql.catalog.tableflow.credential": "{apikey}:{secret}",
           "spark.sql.catalog.tableflow.io-impl": "org.apache.iceberg.aws.s3.S3FileIO",
           "spark.sql.catalog.tableflow.s3.remote-signing-enabled": "true",
           "spark.sql.catalog.tableflow.client.region": "us-east-1"
         }
       }
     }'
   ```

   **Using CPDCTL CLI:**

   ```bash
   cpdctl spark application-submit \
     --engine-id {engine_id} \
     --application s3://bucket/query_tableflow.py \
     --conf spark.sql.catalog.tableflow=org.apache.iceberg.spark.SparkCatalog \
     --conf spark.sql.catalog.tableflow.type=rest \
     --conf spark.sql.catalog.tableflow.uri=https://tableflow.us-east-1.aws.confluent.cloud/iceberg/catalog/organizations/{ORG_ID}/environments/{ENV_ID} \
     --conf spark.sql.catalog.tableflow.credential={apikey}:{secret} \
     --conf spark.sql.catalog.tableflow.io-impl=org.apache.iceberg.aws.s3.S3FileIO \
     --conf spark.sql.catalog.tableflow.s3.remote-signing-enabled=true \
     --conf spark.sql.catalog.tableflow.client.region=us-east-1
   ```

### Results
{: #data_stream_confluent2spark_4}

You can now query remote streaming data from Confluent Tableflow without copying data. The tables automatically reflect new messages published to Kafka topics.


### Example output
{: #data_stream_confluent2spark_5}

   ```bash
   Available namespaces:
   +------------+
   |namespace   |
   +------------+
   |lkc-5g8orq  |
   +------------+

   Tables in lkc-5g8orq:
   +------------+---------+-----------+
   |namespace   |tableName|isTemporary|
   +------------+---------+-----------+
   |lkc-5g8orq  |topic_0  |false      |
   |lkc-5g8orq  |topic_2  |false      |
   +------------+---------+-----------+

   Total rows: 4
   ```

### Related information
{: #data_stream_confluent2spark_6}

- [Integrating Confluent Tableflow](/docs/watsonxdata?topic=watsonxdata-data_stream_confluent1)
- [Querying Confluent Tableflow using Presto engine](/docs/watsonxdata?topic=watsonxdata-data_stream_confluent3presto)
- [Confluent Tableflow documentation](https://docs.confluent.io/cloud/current/topics/tableflow/overview.html)
- [Apache Iceberg documentation](https://iceberg.apache.org/)
