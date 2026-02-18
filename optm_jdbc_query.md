---

copyright:
  years: 2022, 2025
lastupdated: "2026-02-18"

keywords: watsonx.data, spark, analytics, configuring
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Optimizing JDBC metadata queries for Presto engines (Java and C++)
{: #jdbc_metadata_optimization}

When using JDBC metadata APIs with Presto engine, query performance depends on the filters you specify. Understanding how to optimize these queries can significantly reduce execution time.
{: shortdesc}

## About JDBC metadata queries
{: #jdbc_metadata_optimization1}

JDBC metadata methods such as `getColumns()`, `getTables()`, and `getSchemas()` are used by applications to discover database structure programmatically. These methods query the metastore to retrieve information about catalogs, schemas, tables, and columns.

Without proper filtering, metadata queries can take 5-8 minutes or longer to complete, depending on the size of your catalog. This occurs because Presto must enumerate all schemas, tables, and columns by querying the metastore when no filters are specified.


## Best practices
{: #jdbc_metadata_optimization2}

To optimize JDBC metadata query performance, follow these recommendations:

### Always specify schema filters
{: #jdbc_metadata_optimization3}

Limit the metadata scan scope by specifying the schema name. This is the most effective way to improve performance.

When calling JDBC metadata methods:
- Specify the schema name parameter instead of using `null`
- This limits the scope to a single schema
- Reduces query time from 5-8 minutes to under 1 minute

### Add table name filters when possible
{: #jdbc_metadata_optimization4}

Further reduce the metadata scan by specifying table names or patterns.

When you know the specific table or table pattern:
- Specify the table name parameter
- Use table name patterns when appropriate
- This provides the fastest execution time

### Use proper escaping for special characters
{: #jdbc_metadata_optimization5}

Schema and table names containing underscores require proper escaping for exact matching.

For names with underscores:
- Use the escape character (backslash `\`) before underscores
- Example: `gosales\_1021` for exact match of `gosales_1021`
- Without escaping, underscore acts as a wildcard character

### Enumerate schemas individually for multiple schemas
{: #jdbc_metadata_optimization6}

If you need metadata for multiple schemas, query them individually rather than using wildcards.

Recommended approach:
1. First, retrieve the list of schemas using `getSchemas()`
2. Then, query each schema individually with specific schema filters
3. This provides better performance than querying all schemas at once

## Why metadata queries can be slow
{: #jdbc_metadata_optimization7}

Presto's metadata query behavior is determined by how it interacts with the metastore:

- **Exact filters** allow early metadata pruning at the metastore level
- **Wildcard queries** require full catalog enumeration
- **No filters** force Presto to retrieve and process all metadata

This is expected engine behavior. Metadata calls to the metastore can only use filters that are explicitly specified in the query. Without filters, Presto must scan the entire catalog, which takes time proportional to the catalog size.
