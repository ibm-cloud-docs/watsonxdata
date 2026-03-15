---

copyright:
  years: 2022, 2026
lastupdated: "2026-03-15"

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

# Integrating Confluent TableFlow with watsonx.data
{: #data_stream_confluent}

Confluent offers a data streaming platform that acts as a central nervous system for real-time data, enabling businesses to connect, store, and manage data streams across cloud and on-premise environments.

Confluent TableFlow automatically converts Apache Kafka topics into ready-to-query Apache Iceberg tables, enabling real-time, zero-ETL analytics. It eliminates complex data pipelines by materializing data in user-owned or managed storage with automated maintenance.

For more information, see [Confluent TableFlow documentation](https://docs.confluent.io/cloud/current/topics/tableflow/get-started/quick-start-managed-storage.html).

## Before you begin
{: #data_stream_confluent1}

**Confluent requirements:**
- Active Confluent Cloud account
- Kafka cluster created in your preferred AWS region
- Kafka topics with TableFlow enabled
- API key and secret for TableFlow authentication
- REST Catalog endpoint from Confluent TableFlow

**watsonx.data requirements:**
- Provisioned Spark engine or Presto engine
- Network connectivity to Confluent Cloud endpoints

**Storage considerations:**
- **Confluent Managed Storage**: No additional setup required; Confluent manages AWS S3 storage
- **Provider Integration (AWS S3)**: Ensure your Kafka cluster and S3 bucket are in the same AWS region; you need S3 access credentials

**Important limitations:**
- TableFlow tables are read-only from external compute engines
- Write operations (INSERT, CREATE TABLE) are not supported
- Presto engine does not support Confluent Managed Storage (use provider-integrated storage instead)

For more information, see [TableFlow limitations](https://docs.confluent.io/cloud/current/topics/tableflow/overview.html#tableflow-in-ccloud).

---

## Querying Confluent TableFlow tables using Spark engine
{: #data_stream_confluent2}


You can query Confluent TableFlow tables using the watsonx.data Spark engine through SparkLab, REST API, or CPDCTL CLI.

### Configuring Spark to connect to TableFlow
{: #data_stream_confluent3}


1. Obtain your TableFlow credentials:
   - Log in to Confluent Cloud
   - Navigate to your TableFlow-enabled topic
   - Create a new API key and note the key and secret
   - Copy the REST Catalog endpoint

2. Configure Spark catalog properties:

   **For Confluent Managed Storage:**
   ```python
   spark_config = {
       "spark.sql.catalog.tableflow": "org.apache.iceberg.spark.SparkCatalog",
       "spark.sql.catalog.tableflow.type": "rest",
       "spark.sql.catalog.tableflow.uri": "https://tableflow.{CLOUD_REGION}.aws.confluent.cloud/iceberg/catalog/organizations/{ORG_ID}/environments/{ENV_ID}",
       "spark.sql.catalog.tableflow.credential": "<apikey>:<secret>",
       "spark.sql.catalog.tableflow.io-impl": "org.apache.iceberg.aws.s3.S3FileIO",
       "spark.sql.catalog.tableflow.rest-metrics-reporting-enabled": "false",
       "spark.sql.catalog.tableflow.s3.remote-signing-enabled": "true",
       "spark.sql.catalog.tableflow.client.region": "{CLOUD_REGION}"
   }
   ```

   **For Provider Integration (AWS S3):**
   Add these additional properties:
   ```python
   "spark.sql.catalog.tableflow.s3.access-key-id": "<s3-access-key>",
   "spark.sql.catalog.tableflow.s3.secret-access-key": "<s3-secret-key>",
   "spark.sql.catalog.tableflow.s3.region": "{S3_REGION}"
   ```

   Replace placeholders:
   - `{CLOUD_REGION}`: Your Confluent cluster region (e.g., us-east-1)
   - `{ORG_ID}`: Your Confluent organization ID
   - `{ENV_ID}`: Your Confluent environment ID
   - `<apikey>:<secret>`: Your TableFlow API credentials
   - `{S3_REGION}`: Your S3 bucket region (for provider integration)

### Option 1: Using SparkLab (VS Code Development Environment)
{: #data_stream_confluent4}

1. Open SparkLab in watsonx.data
2. Create a new PySpark notebook
3. Add the Spark configuration and query code:

```python
from pyspark.sql import SparkSession

# Create Spark session with TableFlow configuration
spark = (
    SparkSession.builder
    .appName("Query Confluent TableFlow")
    .config("spark.sql.catalog.tableflow", "org.apache.iceberg.spark.SparkCatalog")
    .config("spark.sql.catalog.tableflow.type", "rest")
    .config("spark.sql.catalog.tableflow.uri", "https://tableflow.us-east-1.aws.confluent.cloud/iceberg/catalog/organizations/{ORG_ID}/environments/{ENV_ID}")
    .config("spark.sql.catalog.tableflow.credential", "<apikey>:<secret>")
    .config("spark.sql.catalog.tableflow.io-impl", "org.apache.iceberg.aws.s3.S3FileIO")
    .config("spark.sql.catalog.tableflow.s3.remote-signing-enabled", "true")
    .config("spark.sql.catalog.tableflow.client.region", "us-east-1")
    .getOrCreate()
)

# List available namespaces
spark.sql("SHOW NAMESPACES IN tableflow").show()

# List tables in a namespace
spark.sql("SHOW TABLES IN tableflow.`{namespace}`").show()

# Query a table
df = spark.sql("SELECT * FROM tableflow.`{namespace}`.{table_name} LIMIT 10")
df.show()
```

4. Run the notebook to query your TableFlow tables

For more information, see [VS Code Development Environment - Spark Labs](/docs/watsonxdata?topic=watsonxdata-sparklabs).

### Option 2: Submitting Spark application using REST API
{: #data_stream_confluent5}

1. Create a PySpark script file (e.g., `query_tableflow.py`) with your query logic
2. Submit the application using the Spark Application API:

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
        "spark.sql.catalog.tableflow.uri": "https://tableflow.us-east-1.aws.confluent.cloud/iceberg/catalog/organizations/{ORG_ID}/environments/{ENV_ID}",
        "spark.sql.catalog.tableflow.credential": "{apikey}:{secret}"
      }
    }
  }'
```

For more information, see [Submitting Spark Application by using REST API](/docs/watsonxdata?topic=watsonxdata-spark-api).

### Option 3: Submitting Spark application using CPDCTL CLI
{: #data_stream_confluent6}

1. Create a PySpark script file
2. Submit using CPDCTL:

```bash
cpdctl spark application-submit \
  --engine-id {engine_id} \
  --application s3://bucket/query_tableflow.py \
  --conf spark.sql.catalog.tableflow=org.apache.iceberg.spark.SparkCatalog \
  --conf spark.sql.catalog.tableflow.type=rest \
  --conf spark.sql.catalog.tableflow.uri=https://tableflow.us-east-1.aws.confluent.cloud/iceberg/catalog/organizations/{ORG_ID}/environments/{ENV_ID} \
  --conf spark.sql.catalog.tableflow.credential={apikey}:{secret}
```

For more information, see [Submitting Spark Application by using CPDCTL](/docs/watsonxdata?topic=watsonxdata-spark-cpdctl).

## Querying Confluent TableFlow tables using Presto engine
{: #data_stream_confluent7}


You can query Confluent TableFlow tables using the watsonx.data Presto engine by registering TableFlow as a custom data source.

**Important**: Presto does not support vended-credentials. You must use provider-integrated storage (AWS S3, Azure, or GCS) with explicit credentials. Confluent Managed Storage is not supported with Presto.

### Registering TableFlow as a custom data source
{: #data_stream_confluent8}

1. In the watsonx.data console, go to **Infrastructure manager**
2. Click **Add component** > **Add data source**
3. Select **Custom** as the data source type
4. Enter a name for the data source (e.g., `confluent_tableflow`)
5. Add the following properties:

```properties
connector.name=iceberg
iceberg.catalog.type=REST
iceberg.rest.uri=https://tableflow.{CLOUD_REGION}.aws.confluent.cloud/iceberg/catalog/organizations/{ORG_ID}/environments/{ENV_ID}
iceberg.rest.auth.type=OAUTH2
iceberg.rest.auth.oauth2.credential=<apikey>:<secret>
hive.s3.aws-access-key=<s3-access-key>
hive.s3.aws-secret-key=<s3-secret-key>
```

Replace placeholders with your actual values.

6. Click **Create**

### Associating the data source with a catalog
{: #data_stream_confluent9}

1. Go to **Data manager** > **Catalogs**
2. Click **Create catalog**
3. Select **Iceberg** as the catalog type
4. Enter a catalog name
5. Select your custom data source (`confluent_tableflow`)
6. Click **Create**

### Connecting the catalog to Presto engine
{: #data_stream_confluent10}


1. Go to **Infrastructure manager**
2. Select your Presto engine
3. Click **Associate catalog**
4. Select the catalog you created
5. Click **Associate**

### Querying TableFlow tables
{: #data_stream_confluent11}

1. Open the Query workspace
2. Select your Presto engine
3. Query your TableFlow tables:

```sql
-- List schemas
SHOW SCHEMAS IN confluent_catalog;

-- List tables
SHOW TABLES IN confluent_catalog."{namespace}";

-- Query data
SELECT * FROM confluent_catalog."{namespace}".{table_name} LIMIT 10;
```

### Results

You can now query real-time streaming data from Confluent TableFlow using watsonx.data Spark or Presto engines. The tables automatically reflect new messages published to Kafka topics.

### Related information
- [Confluent TableFlow documentation](https://docs.confluent.io/cloud/current/topics/tableflow/overview.html)
- [Apache Iceberg documentation](https://iceberg.apache.org/)
- [watsonx.data Spark engine](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-spark-engine)
- [watsonx.data Presto engine](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-presto-engine)
