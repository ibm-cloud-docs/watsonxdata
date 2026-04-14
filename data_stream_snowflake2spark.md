---

copyright:
  years: 2022, 2026
lastupdated: "2026-04-14"

keywords: lakehouse, remote data, snowflake, {{site.data.keyword.lakehouse_short}}

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

# Querying Snowflake Open Catalog using Spark engine
{: #data_stream_snowflake2spark}

## About this task
{: #data_stream_snowflake2spark1}

You can query remote Snowflake Tableflow tables using the {{site.data.keyword.lakehouse_full}} Spark engine through zero-copy data federation. Within {{site.data.keyword.lakehouse_short}} Spark, object names are treated as case-insensitive by default. As a result, the use of quoted identifiers is not required when accessing schemas and tables that are created in Snowflake.

For general information about Snowflake Open Catalog integration, see [Integrating Snowflake Open Catalog in {{site.data.keyword.lakehouse_short}}](/docs/watsonxdata?topic=watsonxdata-data_stream_snowflake1).

## Before you begin
{: #data_stream_snowflake2spark2}

Ensure that the following prerequisites are met before proceeding.

**Snowflake requirements:**

- An active Snowflake Open Catalog account
- Access to a Snowflake Query Workspace
- A service connection with a valid client ID and client secret for authentication
- The REST Catalog endpoint associated with your Snowflake Open Catalog account

**{{site.data.keyword.lakehouse_short}} requirements:**

- A provisioned {{site.data.keyword.lakehouse_short}} Spark engine

**Storage requirements:**

- A Google Cloud Storage (GCS) bucket located in the same region as the Snowflake Open Catalog account to ensure optimal performance and compatibility

## Procedure
{: #data_stream_snowflake2spark3}

1. Run the following in Snowflake workspace to create catalog integration

```sql
CREATE OR REPLACE CATALOG INTEGRATION <catalog_integration_name>
  CATALOG_SOURCE=POLARIS
  TABLE_FORMAT=ICEBERG
  REST_CONFIG = (
    CATALOG_URI = '<catalog_uri>'
    CATALOG_NAME = '<open_catalog_name>'
  )
  REST_AUTHENTICATION = (
    TYPE = OAUTH
    OAUTH_CLIENT_ID = 'abc123xyz'
    OAUTH_CLIENT_SECRET = 'secret456def'
    OAUTH_ALLOWED_SCOPES = ('PRINCIPAL_ROLE:ALL')
  )
  ENABLED=TRUE;
```
{: codeblock}

2. Create an external volume by following the steps:
   1. Navigate to Snowflake UI.
   2. Go to **Data** → **Databases** → **External Volumes**.
   3. Click **Configure External Volume**.
   4. Configure with GCS bucket details:
      - **Name:** Choose a descriptive name
      - **Storage Location:** `gs://<gcs_bucket_name>/<path>`
      - **Storage Integration:** Select or create GCS storage integration

3. Create a catalog-linked database.

```sql
CREATE OR REPLACE DATABASE <database_name>
  LINKED_CATALOG = (
    CATALOG = '<catalog_integration_name>'
  )
  EXTERNAL_VOLUME = '<external_volume_name>';
```
{: codeblock}

4. Create a schema if it does not exist.

```sql
CREATE SCHEMA IF NOT EXISTS <database_name>.<catalog_integration_name>;
```
{: codeblock}

Within {{site.data.keyword.lakehouse_short}} Spark, object names are treated as case-insensitive by default. As a result, the use of quoted identifiers is not required when accessing schemas and tables that are created in Snowflake.
{: note}

5. Create Iceberg table.

```sql
CREATE OR REPLACE ICEBERG TABLE <database_name>.<catalog_name>.<table_name>(
  col1 data_type,
  col2 data_type,
  col3 data_type
);
```
{: codeblock}

6. Insert data into the Iceberg table.

```sql
INSERT INTO <database_name>.<catalog_name>.<table_name>
(col1, col2, col3)
VALUES
  ('John', 'Doe', 100, '2024-01-10'),
  ('Jane', 'Smith', 250, '2024-02-15'),
  ('Alice', 'Johnson', 300, '2024-03-20');
```
{: codeblock}

7. Validate the table in Snowflake

```sql
SELECT * FROM <database_name>.<catalog_name>.<table_name>;
```
{: codeblock}

8. Follow the steps to access the table in {{site.data.keyword.lakehouse_short}} using Spark

**Shell Script:**

- Submits Spark applications to the {{site.data.keyword.lakehouse_short}} engine via REST API
- Configures Spark runtime properties
- References the Python application stored in object storage

Shell Script (Generic Template)

```bash
#!/bin/bash
# Spark Iceberg performance test – watsonx.data

app_endpoint="<cpd_cluster_uri>"
engine_id="<engine_id_inside_wxd>"
instance_id="<wxd_instance_id>"
cos_bucket_location="<bucket_location>"
cos_file_path="<file_name>"

app_location="${cos_bucket_location}${cos_file_path}"

app_name="spark_gcs_sf1_$(date +%s)"

confVal='{
  "spark.hadoop.fs.cos.<bucketname>.endpoint":"<endpoint_to_the_bucket>",
  "spark.hadoop.fs.cos.<bucketname>.access.key":"<bucket_access_key>",
  "spark.hadoop.fs.cos.<bucketname>.secret.key":"<bucket_secret_key>",
  "spark.hadoop.google.cloud.auth.service.account.enable": "true",
  "spark.hadoop.google.cloud.auth.service.account.json.keyfile": "<path_to_the_json_key_file_mounted>",
  "spark.sql.parquet.enableVectorizedReader": "false",
  "spark.sql.iceberg.vectorization.enabled": "false",
  "spark.serializer": "org.apache.spark.serializer.KryoSerializer",
  "spark.kryo.registrationRequired": "false",
  "spark.kryo.unsafe": "false",
  "spark.sql.adaptive.enabled": "false",
  "spark.sql.adaptive.coalescePartitions.enabled": "false",
  "spark.sql.catalog.spark_sf_catalog.io-impl": "org.apache.iceberg.hadoop.HadoopFileIO",
  "spark.eventLog.enabled": "true",
  "spark.sql.catalog.spark_sf_catalog.uri": "<snowflake_catalog_uri>",
  "spark.sql.catalog.spark_sf_catalog.warehouse": "<snowflake_catalog_name>",
  "spark.sql.catalog.spark_sf_catalog.scope": "PRINCIPAL_ROLE:<principal_role_of_the_catalog>",
  "spark.sql.catalog.spark_sf_catalog.type": "rest",
  "spark.sql.catalog.spark_sf_catalog": "org.apache.iceberg.spark.SparkCatalog",
  "spark.sql.defaultCatalog": "<catalog_name>",
  "spark.sql.extensions": "org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions",
  "spark.sql.catalog.spark_sf_catalog.credential": "<client_id>:<client_secret>"
}'
```
{: codeblock}

**Python Script:**

- Initializes Spark session
- Connects to the Iceberg REST catalog
- Queries and validates table data

Python script (Generic template)

```python
from pyspark.sql import SparkSession
from pyspark import SparkConf
import os
import logging
from typing import Optional

# Configure logging
logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s - %(levelname)s - %(message)s'
)
logger = logging.getLogger(__name__)

# Constants
CATALOG_NAME = "<catalog_name>"  # Configured in job submission script as defaultCatalog
SCHEMA_NAME = "<schema_name>"
TABLE_NAME = "<table_name>"
GCS_LOCATION = "<gcs_bucket_location>"
CONFIG_FILE_PATH = "<path_to_the_json_key_file>"


def init_spark() -> SparkSession:
    """
    Initialize Spark session with GCS configuration.

    Returns:
        SparkSession: Configured Spark session
    """
    logger.info("Initializing Spark session...")

    conf = SparkConf()

    spark = SparkSession.builder \
        .appName("Snowflake-GCS-Integration") \
        .config(conf=conf) \
        .getOrCreate()

    logger.info("Spark session initialized successfully")
    return spark


def query_table(spark: SparkSession) -> None:
    """
    Query the Snowflake table through Spark.

    Args:
        spark: Active Spark session
    """
    logger.info(f"Querying table: {CATALOG_NAME}.{SCHEMA_NAME}.{TABLE_NAME}")

    # Query the table
    df = spark.sql(f"SELECT * FROM {CATALOG_NAME}.{SCHEMA_NAME}.{TABLE_NAME}")

    # Show results
    logger.info("Query results:")
    df.show()

    # Get row count
    count = df.count()
    logger.info(f"Total rows: {count}")


def main():
    """
    Main execution function.
    """
    try:
        # Initialize Spark session
        spark = init_spark()

        # Query the table
        query_table(spark)

        logger.info("Job completed successfully")

    except Exception as e:
        logger.error(f"Job failed with error: {str(e)}")
        raise
    finally:
        if 'spark' in locals():
            spark.stop()
            logger.info("Spark session stopped")


if __name__ == "__main__":
    main()
```
{: codeblock}

## Results
{: #data_stream_snowflake2spark15}

You can now query Iceberg tables from Snowflake Open Catalog using Spark. The queries execute directly on the data in the external storage location without copying data into {{site.data.keyword.lakehouse_short}}.

## Example queries and outputs
{: #data_stream_snowflake2spark16}

Example Results:

```sql
+---------------+--------------+------------+-----------------+
|FIRST_NAME     |LAST_NAME     |AMOUNT      |CREATE_DATE      |
+---------------+--------------+------------+-----------------+
|John           |Doe           |100         |2024-01-10       |
|Jane           |Smith         |250         |2024-02-15       |
|Alice          |Johnson       |300         |2024-03-20       |
+---------------+--------------+------------+-----------------+
```
{: screen}

## Outcome
{: #data_stream_snowflake2spark17}

The setup enables direct, zero-copy querying of Snowflake Iceberg tables from {{site.data.keyword.lakehouse_short}}, eliminating the need for data replication.

## Related information
{: #data_stream_snowflake2spark18}

- [Integrating Snowflake Open Catalog in {{site.data.keyword.lakehouse_short}}](/docs/watsonxdata?topic=watsonxdata-data_stream_snowflake1)
- [Querying Snowflake Open Catalog using Presto engine](/docs/watsonxdata?topic=watsonxdata-data_stream_snowflake3presto)
- [Snowflake Open Catalog documentation](https://docs.snowflake.com/en/user-guide/tables-iceberg)
- [Apache Iceberg documentation](https://iceberg.apache.org/)
