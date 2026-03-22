---

copyright:
  years: 2022, 2026
lastupdated: "2026-03-22"

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

# Querying Confluent Tableflow using Presto engine
{: #data_stream_confluent3presto}

## About this task
{: #data_stream_confluent3presto_1}

You can query remote Confluent Tableflow tables using the {{site.data.keyword.lakehouse_full}} Presto engine by registering Tableflow as a custom data source for zero-copy data federation.

   Presto does not support vended-credentials. You must use provider-integrated storage (AWS S3, Azure Blob, or Google Cloud Storage) with explicit credentials. Confluent managed storage is not supported with Presto.
   {: important}

## Before you begin
{: #data_stream_confluent3presto_2}

- **Confluent requirements:**
   - Active Confluent Cloud account
   - Kafka cluster with Tableflow-enabled topics using **provider-integrated storage**
   - Tableflow API key and secret
   - REST Catalog endpoint
- **Table information requirements**:
   - List of Kafka topic names with Tableflow enabled
   - Kafka cluster ID (namespace) where topics are located
- **{{site.data.keyword.lakehouse_short}} requirements:**
   - Provisioned Presto engine
   - Network connectivity to Confluent Cloud endpoints
- **Storage requirements:**
   - AWS S3, Azure Blob Storage, or Google Cloud Storage configured as Tableflow storage
   - Storage access credentials (access key and secret key for AWS S3)

## Procedure
{: #data_stream_confluent3presto_3}

1. Register Tableflow as a custom data source for remote lakehouse access.

   1. In the {{site.data.keyword.lakehouse_short}} console, click **Infrastructure manager**.
   2. Click **Add component** > **Add data source**.
   3. Select **Custom** as the data source type.
   4. Enter a display name (e.g., `confluent_tableflow`).
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
      - `{APIKEY}:{SECRET}`: Your Tableflow API credentials
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

   The catalog is now available for querying remote data through the Presto engine.

4. Query Tableflow tables

   1. Click **Query workspace**.
   2. Select your Presto engine from the engine dropdown.
   3. Run queries against your remote Tableflow tables using fully qualified table names:

      ```sql
      -- List available schemas (Kafka cluster IDs)
      SHOW SCHEMAS IN confluent_catalog;

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

You can now query real-time data from Confluent Tableflow using Presto. The tables automatically reflect new messages published to Kafka topics.

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

### Limitations
{: #data_stream_confluent3presto_6}

- Presto cannot automatically discover Tableflow tables.
- Tables do not appear in **Data Manager** or with the `SHOW TABLES` command.
- You must know the exact Kafka topic names and cluster ID to query them.
- Presto requires customer-managed storage (AWS S3, Azure Blob Storage, or Google Cloud Storage) with explicit credentials. Platform-managed storage is not supported.

### Related information
{: #data_stream_confluent3presto_7}

- [Integrating Confluent Tableflow](/docs/watsonxdata?topic=watsonxdata-data_stream_confluent1)
- [Querying Confluent Tableflow using Spark engine](/docs/watsonxdata?topic=watsonxdata-data_stream_confluent2spark)
- [Confluent Tableflow documentation](https://docs.confluent.io/cloud/current/topics/tableflow/overview.html)
- [Presto Iceberg connector](https://prestodb.io/docs/current/connector/iceberg.html)
