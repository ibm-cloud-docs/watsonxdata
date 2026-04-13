---

copyright:
  years: 2022, 2026
lastupdated: "2026-04-13"

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

# Integrating Snowflake Open Catalog in {{site.data.keyword.lakehouse_short}}
{: #data_stream_snowflake1}

Snowflake Open Catalog is a unified governance solution for Apache Iceberg tables in Snowflake. By integrating Snowflake Open Catalog with {{site.data.keyword.lakehouse_full}}, you can query remote Snowflake tables without copying data, enabling seamless data federation across your data landscape.

{{site.data.keyword.lakehouse_short}} supports querying Snowflake Open Catalog tables through:
- **Spark engine** - Query Iceberg tables using PySpark with case-insensitive object names
- **Presto engine** - Query Iceberg tables through the Iceberg REST Catalog API with case-sensitive object names

This integration enables:
- Zero-copy data federation across Snowflake and {{site.data.keyword.lakehouse_short}}
- Unified access to data stored in external locations (Google Cloud Storage)
- Consistent governance and security policies across platforms

## Architecture overview
{: #data_stream_snowflake2}

The integration works through the following components:

1. **Snowflake Open Catalog** - Centralized metadata and governance layer for Iceberg tables
2. **Iceberg REST Catalog API** - Standard interface for accessing table metadata
3. **{{site.data.keyword.lakehouse_short}} engines** - Spark or Presto engines that execute queries
4. **External storage** - Google Cloud Storage where data resides

## Before you begin
{: #data_stream_snowflake3}

**Snowflake requirements:**

Ensure you have the following:

- Active Snowflake Open Catalog account
- Access to a Snowflake Query Workspace
- Authentication credentials:
   - Service connection with a valid client ID and client secret for authentication
- The REST Catalog endpoint associated with your Snowflake Open Catalog account

**Obtaining Snowflake credentials:**

   1. Log in to your Snowflake workspace.
   2. Navigate to **Admin > Security Integrations**.
   3. Create or select a catalog integration with OAuth authentication.
   4. Note the **Client ID** and **Client Secret** for the service connection.
   5. Identify your catalog URI (format: `https://<account>.snowflakecomputing.com/polaris/api/catalog`).
   6. Note your Open Catalog name and database names.

**Snowflake permissions setup:**

Your Snowflake service principal must have the required permissions to access the Open Catalog and its tables:

- **USAGE** privilege on the catalog integration
- **SELECT** privilege on tables you want to query
- **USAGE** privilege on schemas containing the tables

For detailed information on Snowflake permissions, see [Snowflake Access Control](https://docs.snowflake.com/en/user-guide/security-access-control) in the Snowflake documentation.

**{{site.data.keyword.lakehouse_short}} requirements:**

- Provisioned Spark engine (version 3.5 or later) for querying Iceberg tables with case-insensitive object names
- Provisioned Presto engine for querying Iceberg tables with case-sensitive object names
- Network connectivity to Snowflake endpoints

**Storage requirements:**

- Google Cloud Storage (GCS) bucket configured as external volume in Snowflake
- GCS bucket located in the same region as the Snowflake Open Catalog account to ensure optimal performance and compatibility
- Storage access credentials:
   - **Google Cloud Storage:** Service account JSON key file with appropriate permissions

## Object name case sensitivity
{: #data_stream_snowflake4}

Understanding case sensitivity is critical when working with Snowflake tables across different engines:

**Spark engine:**
- Object names (schemas and tables) are treated as **case-insensitive** by default
- Quoted identifiers are not required when accessing schemas and tables created in Snowflake
- Example: `SELECT * FROM database.schema.table` works regardless of the original case

**Presto engine:**
- Object names are treated as **case-sensitive**
- Schemas and tables in Snowflake must be created using **double-quoted identifiers** to preserve the intended case
- Since Presto recognizes object names in lowercase, it is recommended to define all schema and table names in **lowercase within double quotes** to ensure consistent and reliable access
- Example: `CREATE SCHEMA "myschema"` and `SELECT * FROM "myschema"."mytable"`

## Security considerations
{: #data_stream_snowflake5}

**Authentication:**

- **OAuth:** Recommended for production environments with service principal authentication using client ID and client secret
- Ensure credentials are stored securely and rotated regularly

**Data access:**

- All queries execute with the permissions of the authenticated service principal
- Snowflake enforces row-level and column-level security policies
- Storage credentials must have appropriate read permissions on external volumes

## Next steps
{: #data_stream_snowflake6}

- [Querying Snowflake Open Catalog using Spark engine](/docs/watsonxdata?topic=watsonxdata-data_stream_snowflake2spark)
- [Querying Snowflake Open Catalog using Presto engine](/docs/watsonxdata?topic=watsonxdata-data_stream_snowflake3presto)

## Related information
{: #data_stream_snowflake7}

- [Snowflake Open Catalog documentation](https://docs.snowflake.com/en/user-guide/tables-iceberg)
- [Snowflake Access Control](https://docs.snowflake.com/en/user-guide/security-access-control)
- [Apache Iceberg documentation](https://iceberg.apache.org/)
