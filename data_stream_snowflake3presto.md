---

copyright:
  years: 2022, 2026
lastupdated: "2026-04-16"

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

# Querying Snowflake Open Catalog using Presto engine
{: #data_stream_snowflake3presto}

## About this task
{: #data_stream_snowflake3presto1}

You can query remote Snowflake Tableflow tables using the {{site.data.keyword.lakehouse_full}} Presto engine through zero-copy data federation. In {{site.data.keyword.lakehouse_short}} Presto, object names are treated as case-sensitive. Therefore, schemas and tables in Snowflake must be created using double-quoted identifiers to preserve the intended case.

In this context, since Presto recognizes object names in lowercase, it is recommended to define all schema and table names in lowercase within double quotes to ensure consistent and reliable access across the federation layer.

For general information about Snowflake Open Catalog integration, see [Integrating Snowflake Open Catalog in {{site.data.keyword.lakehouse_short}}](/docs/watsonxdata?topic=watsonxdata-data_stream_snowflake1).

## Before you begin
{: #data_stream_snowflake3presto2}

Ensure that the following prerequisites are met before proceeding.

**Snowflake requirements:**

- An active Snowflake Open Catalog account
- Access to a Snowflake Query Workspace
- A service connection with a valid client ID and client secret for authentication
- The REST Catalog endpoint associated with your Snowflake Open Catalog account

**{{site.data.keyword.lakehouse_short}} requirements:**

- A provisioned {{site.data.keyword.lakehouse_short}} Presto engine
- A configured custom storage component
- A configured custom catalog component

**Storage requirements:**

- A Google Cloud Storage (GCS) bucket located in the same region as the Snowflake Open Catalog account to ensure optimal performance and compatibility

## Procedure
{: #data_stream_snowflake3presto3}

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
   2. Go to **Catalog** → **External Data** → **External Volumes**.
   3. Click **create**.
   4. Choose cloud provider as **Google cloud storage** and click **Next**.
   5. Go to Google Cloud console and create a custom role that has the permissions required to access the GCS bucket. Once completed go to Snowflake UI and click **Next**.
   6. Configure with GCS bucket details and click **Next**:
      - **Name:** Choose a descriptive name
      - **Storage Location:** `gcs://<gcs_bucket_name>/<path>`
   7. Once connection is verified, click on **create**.

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
CREATE SCHEMA IF NOT EXISTS <database_name>."<catalog_integration_name>";
```
{: codeblock}

Enclose the catalog name inside double quotes. In this context, since Presto recognizes object names in lowercase, it is recommended to define all schema and table names in lowercase within double quotes to ensure consistent and reliable access across the federation layer.
{: important}

5. Create Iceberg table.

```sql
CREATE OR REPLACE ICEBERG TABLE <database_name>."<catalog_name>"."<table_name>" (
  col1 data_type,
  col2 data_type,
  col3 data_type
);
```
{: codeblock}

6. Insert data into the Iceberg table.

```sql
INSERT INTO <database_name>."<catalog_name>"."<table_name>"
(col1, col2, col3)
VALUES
  ('John', 'Doe', 100, '2024-01-10'),
  ('Jane', 'Smith', 250, '2024-02-15'),
  ('Alice', 'Johnson', 300, '2024-03-20');
```
{: codeblock}

7. Validate the table in Snowflake

```sql
SELECT * FROM <database_name>."<catalog_name>"."<table_name>";
```
{: codeblock}

Enclose the catalog name and table name inside double quotes.
{: note}

8. Enable auto refresh (Metadata sync)

```sql
ALTER ICEBERG TABLE <database_name>."<catalog_name>"."<table_name>"
SET AUTO_REFRESH = TRUE;
```
{: codeblock}


9. Follow the steps to access {{site.data.keyword.lakehouse_short}} and configure GCS Storage.

   **Create or Select Presto Engine:**

   1. Navigate to **{{site.data.keyword.lakehouse_short}}** → **Infrastructure Manager**.
   2. Create a new Presto engine or select an existing one.

   **Add GCS Storage Component:**

   1. Click **Add Component** in Infrastructure Manager.
   2. Select **Storage Component**.
   3. Create a new GCS Storage Bucket.
   4. Provide the GCS endpoint URL.

   **Upload GCS Service Account Key:**

   Upload a JSON key file with the following structure:

   ```json
   {
     "type": "service_account",
     "project_id": "<your_gcs_project_id>",
     "private_key_id": "<your_private_key_id>",
     "private_key": "-----BEGIN PRIVATE KEY-----\n<your_private_key>\n-----END PRIVATE KEY-----\n",
     "client_email": "<service_account_email>",
     "client_id": "<your_client_id>",
     "auth_uri": "https://accounts.google.com/o/oauth2/auth",
     "token_uri": "https://oauth2.googleapis.com/token",
     "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
     "client_x509_cert_url": "<your_cert_url>",
     "universe_domain": "googleapis.com"
   }
   ```
   {: codeblock}

   **Associate Catalog:**

   1. Toggle **Associate Catalog** button to ON.
   2. Create a new catalog to associate with this storage component.

10. In Infrastructure Manager, create a new Custom Data Storage component with the following configuration:

   ```properties
   connector.name=iceberg
   iceberg.catalog.type=rest
   iceberg.rest.uri=<snowflake_polaris_rest_uri>
   iceberg.rest.auth.oauth2.credential=<client_id>:<client_secret>
   iceberg.rest.auth.type=OAUTH2
   iceberg.rest.auth.oauth2.scope=PRINCIPAL_ROLE:writer
   iceberg.catalog.warehouse=<warehouse_name>
   hive.s3.endpoint=https://storage.googleapis.com
   hive.gcs.json-key-file-path=<path_to_gcs_json_key>
   hive.gcs.use-access-token=false
   ```
   {: codeblock}

11. Associate a catalog to this custom component.

12. Go to Query Workspace and follow the instructions:
   a. Navigate to your custom catalog.
   b. Refresh the catalog.
   c. Expand the schema.
   d. Query the table:

      ```sql
      SELECT * FROM <schema_name>.<table_name>;
      ```
      {: codeblock}

## Results
{: #data_stream_snowflake3presto16}

You can now query Iceberg tables from Snowflake Open Catalog using Presto. The queries execute directly on the data in the external storage location without copying data into {{site.data.keyword.lakehouse_short}}.

## Example queries and outputs
{: #data_stream_snowflake3presto17}

Query a table:

```sql
SELECT * FROM <schema_name>.<table_name>;
```
{: codeblock}

Output:

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

## Troubleshooting Tips
{: #data_stream_snowflake3presto18}

- Ensure catalog integration uses correct URI and credentials
- Use `PRINCIPAL_ROLE:ALL` for full visibility
- Refresh {{site.data.keyword.lakehouse_short}} catalog after table creation
- Ensure table is not empty (insert at least one row)

## Related information
{: #data_stream_snowflake3presto19}

- [Integrating Snowflake Open Catalog in {{site.data.keyword.lakehouse_short}}](/docs/watsonxdata?topic=watsonxdata-data_stream_snowflake1)
- [Querying Snowflake Open Catalog using Spark engine](/docs/watsonxdata?topic=watsonxdata-data_stream_snowflake2spark)
- [Snowflake Open Catalog documentation](https://docs.snowflake.com/en/user-guide/tables-iceberg)
- [Presto Iceberg connector](https://prestodb.io/docs/current/connector/iceberg.html)
