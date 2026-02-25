---

copyright:
  years: 2022, 2025
lastupdated: "2026-02-25"

keywords: watsonx.data, spark, analytics, configuring
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Optimizing JDBC metadata queries for Presto (Java and C++) engines
{: #jdbc_metadata_optimization}

Slow performance when querying metadata through Presto JDBC.
{: shortdesc}

## What's happening
{: #jdbc_metadata_optimization1}

Metadata queries using `getColumns(catalog, null, null, "%")` through Presto JDBC might take 5–8 minutes or more to complete.

The `getColumns()` method signature is: `ResultSet getColumns(String catalog, String schemaPattern, String tableNamePattern, String columnNamePattern)`

Where:
- **catalog**: Specify the catalog name exactly as it appears in the database. Use `""` (an empty string) to retrieve entries without a catalog, or use `null` to avoid using the catalog name as a filter.
- **schemaPattern**: Specify the schema name pattern exactly as it appears in the database. Use `""` (an empty string) to retrieve entries without a schema, or use `null` to avoid using the schema name to filter the search.
- **tableNamePattern**: Specify the table name pattern exactly as it appears in the database.
- **columnNamePattern**: Specify the column name pattern exactly as it appears in the database.

When you pass `null` for schema and table parameters, Presto cannot apply any filters at the metastore level, forcing it to scan the entire catalog.

## Why it's happening
{: #jdbc_metadata_optimization2}

This is expected behavior when querying all columns across an entire catalog without filters. The operation requires Presto to enumerate all schemas, tables, and columns by querying the Hive Metastore.

Presto's metadata query behavior is determined by how it interacts with the metastore:

- Exact filters allow early metadata pruning at the metastore level
- Wildcard queries require full catalog enumeration
- No filters force Presto to retrieve and process all metadata

Metadata calls to the metastore can only use filters that are explicitly specified in the query. Without filters, Presto must scan the entire catalog, which takes time proportional to the catalog size.


## How to fix it
{: #jdbc_metadata_optimization3}

Specify filters in your metadata queries and configure metastore caching to improve performance:

### Always specify schema filters
{: #jdbc_metadata_optimization4}

Limit the metadata scan scope by specifying the schema name. This is the most effective way to improve performance.

When calling JDBC metadata methods:

- Specify the schema name parameter instead of using `null`.
- This limits the scope to a single schema.

Example query:

```bash
   getColumns(<catalog_name>, <schema_pattern>, null, "%")

```
{: codeblock}


### Add table name filters when possible
{: #jdbc_metadata_optimization5}

Further reduce the metadata scan by specifying table names or patterns.

When you know the specific table or table pattern:

- Specify the table name parameter.
- Use table name patterns when appropriate. This provides the fastest execution time.

Example query:

```bash
   getColumns(<catalog_name>, <schema_pattern>, <table_pattern>, "%")

```
{: codeblock}

### Use proper escaping for special characters when using `LIKE` operator
{: #jdbc_metadata_optimization6}

Schema and table names containing underscores require proper escaping for exact matching.

For names with underscores:

- Use the escape character (backslash `\`) before underscores. For example: `gosales\_1021` for exact match of `gosales_1021`
- For the `LIKE` operator, when you do not escape, underscore acts as a wildcard character.

   ```bash
   SELECT TABLE_CAT, TABLE_SCHEM, TABLE_NAME, COLUMN_NAME, DATA_TYPE
   FROM system.jdbc.columns
   WHERE TABLE_CAT = 'hive_data' AND TABLE_SCHEM LIKE 'gosales\_1021' ESCAPE '\'

   ```
   {: codeblock}

### Enumerate schemas individually for multiple schemas
{: #jdbc_metadata_optimization7}

If you need metadata for multiple schemas, query them individually rather than using wildcards.

Recommended approach:

1. Retrieve the list of schemas using `getSchemas()`.
2. Query each schema individually with specific schema filters. This provides better performance than querying all schemas at once.

Querying metadata without filters across an entire catalog is not recommended for production use.
{: note}

### Configure metastore caching on coordinator
{: #jdbc_metadata_optimization8}

This section is only applicable for hive catalogs.
{: note}

Configure metastore caching to improve metadata query performance:

- **hive.metastore-cache-scope**: This setting controls whether the system caches only partition‑related metadata or caches all metadata, including partition details, table names, database names, roles, and more. Possible values are `ALL` and `PARTITION`.
- **hive.metastore-cache-ttl**: Specifies the duration for how long you want cached metastore data to be considered valid.
- **hive.metastore-refresh-interval**: Asynchronously refreshes cached metastore data after access when it is older than this interval but not yet expired, allowing subsequent accesses to use fresh data.
- **hive.metastore-cache-maximum-size**: Sets the metastore cache maximum size.

Example sample configuration values for above parameters:

```bash
   hive.metastore-cache-scope=ALL
  hive.metastore-cache-ttl=120m
  hive.metastore-refresh-interval=60m
  hive.metastore-cache-maximum-size=1000
```
