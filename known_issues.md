---

copyright:
  years: 2022, 2024
lastupdated: "2024-04-03"

keywords: lakehouse

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

# Known issues (Limitations)
{: #known_issues}

The following limitations and known issues apply to {{site.data.keyword.lakehouse_full}}.

<!-- ## Issue: Longer `omrgc_spinlock_acquire` calls slow down {{site.data.keyword.lakehouse_short}} performance
{: #known_issues1.0.0_7}

As a result of Intel's CPU upgrade, the `omrgc_spinlock_acquire` call takes longer to complete, making {{site.data.keyword.lakehouse_short}} slower. -->
<!--
**Workaround:**: Do the following steps:

   1. Go to Presto folder path (/opt/presto/etc folder).
   2. Update the jvm.config file to include the new JVM parameter, `-Xgc:tlhInitialSize=8096,tlhIncrementSize=16384,tlhMaximumSize=1048576`.
   3. Restart the Presto coordinator and worker node. -->


## Issue: Milvus unresponsive to queries
{: #known_issues9946}

Milvus may not respond to queries when attempting to load collections or partitions that exceed available memory capacity. This occurs because all search and query operations within Milvus are executed in memory, requiring the entire collection or partition to be loaded before querying.

**Workaround:**

* Consider the memory limitations of your Milvus deployment and avoid loading excessively large collections or partitions.

* If Milvus becomes unresponsive to queries, employ the appropriate Milvus API to unload or release some collections from memory. An example using Python SDK: `collection.release()`

## Issue: Inaccurate row count after deletions in Milvus
{: #known_issues9947}

The `collection.num_entities` property might not reflect the actual number of rows in a Milvus collection after deletion operations. This property provides an estimate and may not account for deleted entities.

To get an accurate count of rows, execute a `count(*)` query on the collection. This provides an accurate count even after deletions.

Pymilvus syntax:
```bash
collection = pymilvus.Collection(...)
collection.query(expr='', fields=['count(*)'])
```
{: codeblock}

## Issue: Potential data loss during batch insert of large data collection in Milvus
{: #known_issues9484}

Potential data loss may occur when inserting large dataset (5 million vectors) through the Milvus batch insert API with a single final flush. A subset of rows might be missing from the ingested data.

**Workaround:**
* Flush the collection manually every 500,000 rows.
* Use the bulk insert API for data ingestion, see [Insert Entities from Files](https://milvus.io/docs/v2.3.x/bulk_insert.md). This is the recommended way to ingest large data sets.

## Issue: Case sensitivity of column names in queries
{: #known_issues7248}

Queries referencing column names are case-insensitive. The results will display columns using the exact casing provided in the query, regardless of the actual casing in the database.

## Limitations: Unsupported Db2 operations
{: #known_issues7895}

{{site.data.keyword.lakehouse_short}} currently does not support the ALTER TABLE DROP COLUMN operation for Db2 column-organized tables.

   By default, Db2 instances create tables in column-organized format.
   {: note}

{{site.data.keyword.lakehouse_short}} does not support creating row-organized tables in Db2.

## Limitations: Handling Null Values in Elasticsearch
{: #known_issues8294}

**Elasticsearch** connector requires explicit definition of index mappings for fields to handle null values when loading data.

## Limitations: Loading Nested JSON with Elasticsearch
{: #known_issues8294(2)}

**Elasticsearch** connector requires users to explicitly specify nested JSON structures as arrays of type ROW for proper loading and querying. To process such structures, use the UNNEST operation.

## Limitation: Users can create 3 instances of Milvus service for a single instance of watsonx.data in IBM Cloud.
{: #known_issues6821}

## Issue: Unrestricted access to SQL statements in worksheets
{: #known_issues18111}

SQL statements within worksheets can be shared with all users who have access to the instance. These statements could be viewed, edited, or deleted by any of these users.

## Issue: Unable to create views in Presto
{: #known_issues1.0.0_6}

Presto describes a view in a mapped database as a TABLE rather than a VIEW. This is apparent to JDBC program connecting to the Presto engine.

## Issue: Connections to MongoDB or MySQL database catalog fails
{: #known_issues1.0.0_5}

When {{site.data.keyword.lakehouse_short}} is upgraded to Version 1.1.0, the user is unable to access the MySQL or MongoDB database catalog, if SSL is enabled for those connections before upgrade. As a workaround, after you upgrade {{site.data.keyword.lakehouse_short}}, remove and readd the SSL-enabled connections to MySQL or MongoDB databases by providing an SSL certificate file. For more information, see [Adding a database](watsonxdata?topic=watsonxdata-reg_database).

## Issue: Using special characters in schema, table, or column names
{: #known_issues1.0.0_4}

It is recommended to not use special characters such as question mark (?) or asterisk (*) in table, column names and schema names. Though these special characters are supported and tables, columns and schemas can be created, using these special characters might cause issues when running the `INSERT` command.

## Issue: User is not removed from the catalog access control on revoking data access
{: #known_issues1.0.0_3}

When you grant user access to a user by adding them to the data control policies by using the **Access Control** screen, the user is successfully listed against the catalog. On revoking user access from the **Access Control** page, the user stays listed against the catalog and continues to have user access.

## Issue: Unable to view expected catalogs from Presto
{: #known_issues1.0.0_2}

Users with administrator privileges are unable to view the expected Hive and PostgreSQL catalogs from Presto.

## Issue: Console UI lists invalid users
{: #known_issues1.0.0_1}

{{site.data.keyword.lakehouse_short}} user (user1) invites a new user (user2) to the account by using the **Manage access and users** screen (**Manage > Access (IAM) > Manage access and users**) and grants access to a role (MetastoreAccess, Viewer, Operator, Editor, Administrator). User2 gets access to resources in the {{site.data.keyword.lakehouse_short}} instance through user1's account. Additionally, user2 is granted data access at the resource level by adding to the data control policies by using the **Access Control** screen.
When user1 removes user2 from the user1's account, user2 is still listed in the **Access Control** tab at resource level.


## Issue: Unable to view created schema
{: #known_issues1}

When a user with the User role and the Create access (the user only has the Create access) is added to an external database, they cannot see the schemas that they created. Though the user can create schemas, they cannot view them. The following is the system response:

```bash
presto:default> show schemas;
Schema
--------
(0 rows)
```
{: codeblock}

**Workaround:** Provide select privilege for the schema the user created.

## Issue: Access denied when querying an external database
{: #known_issues2}

When a user with the User role and Create access (the user only has Create access), is added to an external database, they cannot run the select query from the table they have created. Though the user can connect to the Presto engine and create tables and schemas, they cannot query from the table. The system displays a `Access Denied` message.

```bash
Query 20230608_132213_00042_wpmk2 failed: Access Denied: Cannot select from columns [id] in table or view tab_appiduser_01
```
{: codeblock}

**Workaround:** Provide select privilege for the table the user created.

## Issue: Schema created under different catalog
{: #known_issues5}

Schemas are available across Iceberg and Hive catalogs. When a schema is created under Iceberg catalog, it is listed under Hive catalog and vice versa.

## Issue: Presto does not support deletion of Iceberg tables
{: #known_issues6}

## Issue: DROP SCHEMA in Db2
{: #known_issues7}

In Db2, the schema can be dropped only if it is empty. Initiating `DROP SCHEMA` statement against a non-empty schema may result in Db2 SQL Error `SQLCODE=-478` and `SQLSTATE=42893`.

## Issue: CREATE VIEW statement that is partially supported by Db2
{: #known_issues8}

Db2 connector partially supports `CREATE VIEW` statement. The Presto supported SQL syntax does not include creating views with custom column names (different than the table column names).

## Issue: CREATE VIEW statement that is partially supported by {{site.data.keyword.netezza_short}}
{: #known_issues9}

{{site.data.keyword.netezza_short}} connector partially supports `CREATE VIEW` statement. The Presto Supported SQL syntax does not include creating views with custom column names (different than the table column names).

## Issue: Presto does not recognize the path as a directory
{: #known_issues12}

When you create a new table with a Presto Hive connector that uses an S3 folder from an external location, Presto does not recognize the path as a directory and an error might occur.

For example, when creating a customer table in the target directory `DBCERT/tbint` in a bucket that is called `dqmdbcertpq` by using the IBM Cloud UX and Aspera S3 console, the following error is encountered: `External location must be a directory`.

```bash
CREATE TABLE "hive-beta"."dbcert"."tbint" (
RNUM int , CBINT bigint
) WITH (
format='PARQUET', external_location = 's3a://dqmdbcertpq/DBCERT/tbint'
);
Query 20230509_113537_00355_cn58z failed: External location must be a directory
```
{: codeblock}

Objects in a file system are stored as objects and their path. The object and path must have an associated metadata. If the path is not associated with the metadata, Presto fails to recognize the object and responds that the path is not a directory.

## Issue: Assigning Grant or Revoke privilege
{: #known_issues13}

Assigning **Grant** or **Revoke** privilege to a user through access policy does not work as expected in the following scenarios:

1. User_A adds a bucket and a Hive catalog (for example, `useracat02`).
2. User_A creates a schema and a table.
3. User_B and User_C are assigned **User** roles to the catalog.
4. User_A adds allow grant policy to User_B.
5. User_B connects to the catalog and runs `grant select` to User_C.

   ```sql
   presto:default> grant select on useracat02.schema_test_01.tab_1 to "6ff74bf7-b71b-42f2-88d9-a98fdbaed304";
   ```
   {: codeblock}

6. When the User_C connects to the catalog and runs `select` command on the table, the command fails with access denied message.

   ```sql
   presto:default> select * from useracat02.schema_test_01.tab_1;
   Query 20230612_073938_00132_hthnz failed: Access Denied: Cannot select from columns [name, id, salary, age] in table or view tab_1
   ```
   {: codeblock}

## Issue: Creating schema without a location
{: #known_issues14}

When you create a schema without a location, it is not listed in the schema list of any catalog.
For example, if you create a schema without specifying the location of the bucket, the schema is created in HMS and not in the bucket. When you try to create a new schema with the same name, it fails and responds that the schema already exists.

**Workaround:** Specify the location of the bucket when creating a schema.

## Issue: Unique names for schema and bucket
{: #known_issues15}

A schema and a bucket cannot be created with the same name.
For example, if you create a schema that is named “sales” in one catalog, the same name cannot be used for another schema in another catalog. Similarly, if you register a bucket with the name “salesbucket”, another bucket with the same cannot be registered, even if the bucket is located in a different object store.

**Workaround:** Use unique names when creating schemas and buckets.

## Issue: Creating schema for target table
{: #known_issues17}

You must create schema for the target table if the schema does not exist.

## Issue: Ingestion fails if CSV file contains bad record
{: #known_issues18}

**ibm-lh** tool does not support skipping maximum bad records for CSV files if the mismatch field is greater than the table definition.

## Issue: Creating schema location with path
{: #known_issues19}

Use one of the following location options when creating a schema:

- Location pointing to a bucket/subpath without a trailing `/`.
- Location pointing to a bucket/subpath with a trailing `/` – Recommended for better structuring.

Though you can use a location pointing to a bucket only with or without a trailing `/`, it might lead to failure. Therefore, it is recommended to use a subpath.
{: note}

## Issue: Presto do not support `AS OF` with iceberg tables
{: #known_issues21}

Presto do not support `AS OF <time stamp>` command in a SELECT query.

**Workaround:** Invoke `CALL iceberg_data_rollback_to_snapshot` to move to the required timestamp.

If you use `CALL iceberg_data_rollback_to_snapshot` with a timestamp, you cannot call the stored procedure to move to a later timestamp. Use Spark SQL as an alternative.
{: note}

## Issue: Only the creator has DROP access on the table in Apache Hive (API)
{: #known_issues22}

Only the creator of a table can drop the table that is created in the Apache Hive catalog. Other users cannot drop the table even if they have an explicit DROP access to the table. They get the `Access Denied` message.

## Issue: User-provided certificates are not supported by {{site.data.keyword.lakehouse_short}}
{: #known_issues23}

Currently, user-provided certificates are not supported in {{site.data.keyword.lakehouse_short}} when adding database connections, object store buckets, or when using ibm-lh utility.

## Issue: No columns to parse from file error
{: #known_issues25}

When you try to ingest folder from AWS S3 using the **ibm-lh** tool, the following error may be encountered if there are no empty files in the folder:

```bash
No columns to parse from file
```
{: screen}

**Workaround:** First list the folders inside the bucket by using `aws s3 ls` command. If no empty files are listed, copy all the files to another folder by using `aws s3 cp` command.

## Test connection with SSL enabled is not supported
{: #known_issues28}

When a user enables SSL connection for data sources, the test connection is not supported through the web console.

## Special characters in target table names can cause ingestion failures
{: #known_issues30}

If a target table name contains special characters such as "`.`", "`,`", "`(`", "`!`" etc, ingestion into the table will fail.

## Limitation: Presto does not support `VARBINARY` datatype
{: #known_issues31}

The current version of Presto does not support binary strings with length. Execution of an `ALTER TABLE` statement on a database results in the following error:

`Unknown type 'varbinary(n)' for column 'testcolumn'`

This is a limitation in Preso and not a limitation in {{site.data.keyword.lakehouse_short}}.
{: note}
