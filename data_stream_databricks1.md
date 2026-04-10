---

copyright:
  years: 2022, 2026
lastupdated: "2026-04-09"

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

# Integrating Databricks Unity Catalog in {{site.data.keyword.lakehouse_short}}
{: #data_stream_databricks1}

Databricks Unity Catalog is a unified governance solution for data and AI assets in Databricks. By integrating Unity Catalog with {{site.data.keyword.lakehouse_full}}, you can query remote Databricks tables without copying data, enabling seamless data federation across your data landscape.

{{site.data.keyword.lakehouse_short}} supports querying Databricks Unity Catalog tables through:
- **Spark engine** - Query both Delta Lake and Iceberg tables using PySpark
- **Presto engine** - Query Iceberg tables and Uniform-enabled Delta tables through the Iceberg REST Catalog API

This integration enables:
- Zero-copy data federation across Databricks and {{site.data.keyword.lakehouse_short}}
- Unified access to data stored in external locations (AWS S3 and Azure Data Lake Storage Gen2)
- Consistent governance and security policies across platforms

## Architecture overview
{: #data_stream_databricks2}

The integration works through the following components:

1. **Databricks Unity Catalog** - Centralized metadata and governance layer
2. **Iceberg REST Catalog API** - Standard interface for accessing table metadata
3. **{{site.data.keyword.lakehouse_short}} engines** - Spark or Presto engines that execute queries
4. **External storage** - AWS S3 and Azure Data Lake Storage Gen2 where data resides

## Before you begin
{: #data_stream_databricks3}

**Databricks requirements:**

Ensure you have the following:

- Active Databricks workspace with Unity Catalog enabled
- Unity Catalog with tables (Delta Lake or Iceberg format)
- Authentication credentials:
   - OAuth credentials (Client ID and Client Secret) for service principal authentication, OR
   - Personal Access Token (PAT) for authentication
- Unity Catalog REST endpoint

**Obtaining Databricks credentials:**

   1. Log in to your Databricks workspace.
   2. Navigate to **Settings > Identity and access**.
   3. Click **Manage** on **Service principals**.
   4. Click **Add service principal** and create a new OAuth application.
   5. Note the **Client ID** and **Client Secret**.
   6. Alternatively, generate a Personal Access Token:
      - Go to **User Settings > Developer > Manage** on **Access Tokens**.
      - Click **Generate new token**.
      - Ensure the token has the `unity-catalog` API scope.
   7. Note your workspace URL (format: `https://<workspace-id>.cloud.databricks.com`).
   8. Identify your catalog name, schema name, and table names.

**Databricks permissions setup:**

Your Databricks service principal or user must have the required Unity Catalog privileges. Unity Catalog uses a hierarchical permission model where privileges granted at higher levels (catalog) automatically apply to lower levels (schemas and tables).

**Understanding privilege inheritance:**

Unity Catalog follows a hierarchical privilege model:

- Catalog-level privileges automatically grant access to all schemas and tables within that catalog
- Schema-level privileges automatically grant access to all tables within that schema
- You can grant privileges at any level depending on your security requirements

For detailed information on privilege inheritance, see [Unity Catalog privilege inheritance](https://docs.databricks.com/data-governance/unity-catalog/manage-privileges/privileges.html) in the Databricks documentation.

**Simplified catalog-level grants (Recommended for testing):**

Grant all privileges at the catalog level for broad access to all schemas and tables:

   1. Log in to your Databricks workspace.
   2. Navigate to **Catalog** in the left sidebar.
   3. Select your catalog, then click the **Permissions** tab.
   4. Click **Grant** and add your service principal or user.
   5. Assign the following privileges at the catalog level:
      - **USE CATALOG** - Access to the catalog and all its schemas
      - **USE SCHEMA** - Access to all schemas within the catalog
      - **SELECT** - Read data from all tables in all schemas
      - **EXTERNAL USE SCHEMA** - Access all schemas with external storage locations (required if using external storage)

**Granular multi-level grants (Recommended for production):**

For fine-grained access control, grant privileges at specific levels:

   **Catalog level:**

      1. Navigate to **Catalog** → **Select your catalog** → **Permissions** tab**.
      2. Grant **USE CATALOG** to allow access to the catalog.

   **Schema level:**

      1. Navigate to **Catalog** → **Select your catalog** → **Select a schema** → **Permissions** tab.
      2. Grant **USE SCHEMA** and **EXTERNAL USE SCHEMA** (if using external storage) for specific schemas.

   **Table level:**

      1. Navigate to **Catalog** → **Select your catalog** → **Select a schema** → **Select a table** → **Permissions** tab**.
      2. Grant **SELECT** on specific tables you want to query.

For detailed information on Unity Catalog permissions, see [Unity Catalog privileges and securable objects](https://docs.databricks.com/data-governance/unity-catalog/manage-privileges/privileges.html) in the Databricks documentation.

**{{site.data.keyword.lakehouse_short}} requirements:**

- Provisioned Spark engine (version 3.5 or later) for querying Delta Lake and Iceberg tables
- Provisioned Presto engine for querying Iceberg tables
- Network connectivity to Databricks workspace endpoints

**Storage requirements:**

- AWS S3 and Azure Data Lake Storage Gen2 configured as external location in Databricks
- Storage access credentials:
   - **AWS S3:** Access key and secret key, S3 region information
   - **Azure Data Lake Storage Gen2:** Storage account name and access key

## Security considerations
{: #data_stream_databricks5}


**Authentication:**

- **OAuth (Spark only):** Recommended for production environments with service principal authentication
- **Personal Access Token:** Suitable for development and testing; ensure tokens are rotated regularly

**Data access:**

- All queries execute with the permissions of the authenticated user or service principal
- Unity Catalog enforces row-level and column-level security policies
- Storage credentials must have appropriate read permissions on external locations

## Next steps
{: #data_stream_databricks7}

- [Querying Databricks Unity Catalog using Spark engine](/docs/watsonxdata?topic=watsonxdata-data_stream_databricks2spark)
- [Querying Databricks Iceberg tables using Presto engine](/docs/watsonxdata?topic=watsonxdata-data_stream_databricks3presto)

## Related information
{: #data_stream_databricks8}

- [Databricks Unity Catalog documentation](https://docs.databricks.com/data-governance/unity-catalog/index.html)
- [Unity Catalog privileges and securable objects](https://docs.databricks.com/data-governance/unity-catalog/manage-privileges/privileges.html)
- [Apache Iceberg documentation](https://iceberg.apache.org/)
