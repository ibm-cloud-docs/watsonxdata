---

copyright:
  years: 2022, 2026
lastupdated: "2026-03-16"

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

# Querying Confluent Tableflow using Presto engine
{: #data_stream_confluent3presto}

## About this task
{: #data_stream_confluent3presto_1}

You can query Confluent Tableflow tables using the {{site.data.keyword.lakehouse_full}} Presto engine by registering Tableflow as a custom data source.

   Presto does not support vended-credentials. You must use provider-integrated storage (AWS S3, Azure Blob, or Google Cloud Storage) with explicit credentials. Confluent Managed Storage is not supported with Presto.
   {: important}

## Before you begin
{: #data_stream_confluent3presto_2}

**Confluent requirements:**
- Active Confluent Cloud account
- Kafka cluster with Tableflow-enabled topics using **provider-integrated storage** (not Confluent Managed Storage)
- Tableflow API key and secret
- REST Catalog endpoint

**{{site.data.keyword.lakehouse_short}} requirements:**
- Provisioned Presto engine
- Network connectivity to Confluent Cloud endpoints

**Storage requirements:**
- AWS S3, Azure Blob Storage, or Google Cloud Storage configured as Tableflow storage
- Storage access credentials (access key and secret key for AWS S3)

## Procedure
{: #data_stream_confluent3presto_3}

1. Register Tableflow as a custom data source.

   1. In the {{site.data.keyword.lakehouse_short}} console, click **Infrastructure manager**
   2. Click **Add component** > **Add data source**
   3. Select **Custom** as the data source type
   4. Enter a display name (e.g., `confluent_tableflow`)
   5. In the **Properties** section, add the following properties:

      ```properties
      connector.name=iceberg
      iceberg.catalog.type=REST
      iceberg.rest.uri=https://tableflow.{CLOUD_REGION}.aws.confluent.cloud/iceberg/catalog/organizations/{ORG_ID}/environments/{ENV_ID}
      iceberg.rest.auth.type=OAUTH2
      iceberg.rest.auth.oauth2.credential={APIKEY}:{SECRET}
      hive.s3.aws-access-key={S3_ACCESS_KEY}
      hive.s3.aws-secret-key={S3_SECRET_KEY}
      ```

      Replace the placeholders:
      - `{CLOUD_REGION}`: Your Confluent cluster region (e.g., `us-east-1`)
      - `{ORG_ID}`: Your Confluent organization ID
      - `{ENV_ID}`: Your Confluent environment ID
      - `{APIKEY}:{SECRET}`: Your TableFlow API credentials
      - `{S3_ACCESS_KEY}`, `{S3_SECRET_KEY}`: Your S3 access credentials

   6. Click **Create**.

2. Create a catalog for the data source.

   1. Click **Data manager** > **Catalogs**.
   2. Click **Create catalog**.
   3. Select **Iceberg** as the catalog type.
   4. Enter a catalog name (e.g., `confluent_catalog`).
   5. In the **Data source** field, select the custom data source you created (`confluent_tableflow`).
   6. Click **Create**.

3. Associate the catalog with Presto engine.

   1. Click **Infrastructure manager**.
   2. Select your Presto engine from the list.
   3. Click **Associate catalog**.
   4. Select the catalog you created (`confluent_catalog`).
   5. Click **Associate**.

   The catalog is now available for querying through the Presto engine.

4. Query TableFlow tables

   1. Click **Query workspace**
   2. Select your Presto engine from the engine dropdown
   3. Run queries against your TableFlow tables:

      ```sql
      -- List available schemas (Kafka cluster IDs)
      SHOW SCHEMAS IN confluent_catalog;

      -- List tables in a schema
      SHOW TABLES IN confluent_catalog."{namespace}";

      -- Describe table structure
      DESCRIBE confluent_catalog."{namespace}".{table_name};

      -- Query data
      SELECT * FROM confluent_catalog."{namespace}".{table_name} LIMIT 10;

      -- Get row count
      SELECT COUNT(*) FROM confluent_catalog."{namespace}".{table_name};
      ```

   Namespace names (Kafka cluster IDs) often contain hyphens and must be enclosed in double quotes.
   {: note}

### Results
{: #data_stream_confluent3presto_4}

You can now query real-time streaming data from Confluent Tableflow using Presto. The tables automatically reflect new messages published to Kafka topics.

### Example queries
{: #data_stream_confluent3presto_5}

   ```sql
   -- List schemas
   SHOW SCHEMAS IN confluent_catalog;

   -- Result:
   -- lkc-5g8orq

   -- Query a table
   SELECT
       my_field1,
       my_field2,
       my_field3,
       "$$timestamp"
   FROM confluent_catalog."lkc-5g8orq".topic_0
   LIMIT 5;
   ```

### Troubleshooting
{: #data_stream_confluent3presto_6}

**Issue**: Cannot connect to TableFlow
- Verify your API credentials are correct
- Ensure the REST catalog endpoint URL is accurate
- Check network connectivity to Confluent Cloud

**Issue**: Authentication failures
- Confirm you're using provider-integrated storage (not Confluent Managed Storage)
- Verify S3 access credentials are valid
- Ensure the S3 bucket region matches your Kafka cluster region

### Related information
{: #data_stream_confluent3presto_7}

- [Integrating Confluent Tableflow](/docs/watsonxdata?topic=watsonxdata-data_stream_confluent1)
- [Querying Confluent Tableflow using Spark engine](/docs/watsonxdata?topic=watsonxdata-data_stream_confluent2spark)
- [Confluent TableFlow documentation](https://docs.confluent.io/cloud/current/topics/tableflow/overview.html)
- [Presto Iceberg connector](https://prestodb.io/docs/current/connector/iceberg.html)
