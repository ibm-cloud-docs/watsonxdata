---

copyright:
  years: 2022, 2023
lastupdated: "2023-07-07"

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

The following limitations and known issues, apply to {{site.data.keyword.lakehouse_full}}.

## Issue: Unable to view created schema
{: #known_issues1}

When a user with the user role and the create privilege (the user only has the create privilege) is added to an external database, they are unable to see the schemas they have created. Though the user can successfully create schemas, they are unable to view them. The following displays the system response:

```bash
presto:default> show schemas;
Schema
--------
(0 rows)
```
{: codeblock}

**Workaround:** You can provide select privilege for the schema that the user created.

## Issue: Access denied message occurs when querying an external database
{: #known_issues2}

When a user with the user role and the create privilege (the user only has the create privilege) is added to an external database, they are unable to run the select query from the table they have created. Though the user can successfully connect to the Presto engine and create tables and schemas, they are unable to execute query from table. The system displays an "Access Denied" message.

```bash
Query 20230608_132213_00042_wpmk2 failed: Access Denied: Cannot select from columns [id] in table or view tab_appiduser_01
```
{: codeblock}

**Workaround:** You can provide select privilege for the table that the user created.

## Issue: System fails to display table columns while creating a policy for a table
{: #known_issues4}

When you create a policy for the table that has a thousand columns, the table columns are not displayed and it generates error message "AMS API failed".

## Issue: Schema created under different catalog
{: #known_issues5}

Schemas are available across Iceberg and Hive catalogs. When a schema is created under Iceberg catalog, it is listed under Hive catalog and vice versa.

## Issue: Presto do not support deletion of Iceberg tables
{: #known_issues6}

## Issue: DROP SCHEMA in Db2
{: #known_issues7}

In Db2, the schema can be dropped only if it is empty. Initiating `DROP SCHEMA` statement against a non-empty schema is expected to result in Db2 SQL Error `SQLCODE=-478` and `SQLSTATE=42893`.

## Issue: CREATE VIEW statement partially supported by DB2
{: #known_issues8}

Db2 connector partially supports `CREATE VIEW` statement. The Presto supported SQL syntax does not include creating views with custom column names (different than the table column names).

## Issue: CREATE VIEW statement partially supported by Netezza
{: #known_issues9}

Netezza connector partially supports `CREATE VIEW` statement. The Presto Supported SQL syntax does not include creating views with custom column names (different than the table column names).

## Issue: Data ingestion through CLI
{: #known_issues10}

* Schema evolution is not supported.
* Partitioning is not supported.
* Iceberg target table is the supported output format.
* Source csv file containing TAB or space as delimiter is not supported.
* pathStyleAccess property for object storage is not supported.
* Source files must be of the same format type and only Parquet and csv file formats are supported.

## Issue: Data ingestion through web console
{: #known_issues11}

* Only Iceberg target table format is supported.
* Partitioning is not supported.
* Source csv file containing TAB or space as delimiter is not supported.
* Configure options are disabled for GA.
* Target table output format is Iceberg and the target data format is in Parquet.
* Target storage path is default and cannot be selected.

## Issue: Presto does not recognize the path as a directory
{: #known_issues12}

When you create a new table with a Presto Hive connector that uses an S3 folder from an external location, presto does not recognize the path as a directory and an error might occur.

For example, if you try to create a customer table in the target directory `DBCERT/tbint` in a bucket called `dqmdbcertpq` by using the IBM Cloud UX and Aspera S3 console, it gives you an error `External location must be a directory`.

```bash
CREATE TABLE "hive-beta"."dbcert"."tbint" (
RNUM int , CBINT bigint
) WITH (
format='PARQUET', external_location = 's3a://dqmdbcertpq/DBCERT/tbint'
);
Query 20230509_113537_00355_cn58z failed: External location must be a directory
```
{: codeblock}

Objects in a file system are stored as objects and their path. The object and path must have an associated metadata. If the path is not associated with the metadata, the Presto fails to recognize the object and responds that the path is not a directory.

## Issue: Assigning Grant or Revoke privilege
{: #known_issues13}

Assigning **Grant** or **Revoke** privilege to a user through access policy does not work as expected in the following scenarios:


1. User_A adds a bucket and a Hive catalog (for example, `useracat02`).
2. User_A creates a schema and a table.
3. User_B and User_C are assigned **User** role to the catalog.
4. User_A adds allow grant policy to User_B
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

When you create a schema without location, it is not listed in the schema list of any catalog.
For example: If you try to create a schema without specifying the location of a bucket, the schema might be getting created in HMS and not in a bucket. Hence, when you try to create a new schema with the same name, it fails and responds that the schema already exists.

**Workaround:** You must make sure that the location of the bucket is specified while creating a schema.

## Issue: Unique names for schema and bucket
{: #known_issues15}

You can not create a schema or a bucket with a similar name.
For example: If you create a schema called "sales" in one catalog, you or another user cannot use the same name for a schema in another catalog.
Similarly, if you registers a bucket with a name 'salesbucket', you or another user cannot register another bucket with the same name even if the bucket is located in a different Object Store.

**Workaround:** You must make sure to create unique names while creating schemas and buckets.

## Issue: Define class error and Name or service not known
{: #known_issues16}

If you restart engine, you will get this define class error com.googlecode.aviator.exception.CompileExpressionErrorException. This error pops up only once and for the first action you perform after the engine restart.

**Workaround:** if you see any of the define class error or name or service not known error, you must wait for a few minutes for the server to completely restart. Then, retry the query for successful execution.

## Issue: Creating schema for target table
{: #known_issues17}

You must create schema for the target table if the schema does not exist.

## Issue: Ingestion fails if CSV file contains bad record
{: #known_issues18}

**ibm-lh** tool does not support skipping maximum bad records for CSV files if the mismatch field is greater than the table definition.

## Issue: Creating schema location with path
{: #known_issues19}

You can create schema in the following ways:

- Create a schema with a location pointing to a bucket without a trailing '/'.
- Create a schema with a location pointing to a bucket with a trailing '/'.
- Create a schema with a location pointing to a bucket/subpath without a trailing '/'.
- Create a schema with a location pointing to a bucket/subpath with a trailing '/'.

**Workaround:** It is recommended to use the third and fourth options. The fourth option is best recommended for better structuring. The first two options are not to be used as it results in a failure.

## Issue: Creating the database of type Memory gives an error
{: #known_issues20}

Creating a database of the type Memory gives an error, `pq: invalid input syntax for type integer: ""`.

## Issue: Presto does not support `AS OF` with iceberg tables
{: #known_issues21}

- Presto does not support `AS OF <time stamp>` in a SELECT query.
- **Workaround:** Invoke CALL iceberg_data_rollback_to_snapshot’ to move to the desired timestamp.
- Once you have called ‘CALL iceberg_data_rollback_to_snapshot’ with a timestamp, you cannot call the stored procedure to move to a later timestamp.
- Use Spark SQL, as an alternative.

## Issue: Only the creator has DROP access on the table in Apache Hive (API)
{: #known_issues22}

Only the creator of a table can drop the tables that are created in Apache hive catalog. Users other than the creator of the table will get an ‘Access denied’ error even if they have been granted an explicit DROP privilege access on the table.

## Issue: User provided certificates are not supported by {{site.data.keyword.lakehouse_short}}
{: #known_issues23}

User provided certificates are not supported in {{site.data.keyword.lakehouse_short}} when adding database connections, object store buckets, or by using ibm-lh utility.

## Issue: CTAS query that uses Parquet format fails
{: #known_issues24}

When you do a CTAS operation to Iceberg tables in Parquet format, you may get the following error:

```bash
Size is greater than maximum int value
```
{: screen}

**Workaround:** Use the presto-cli to do the CTAS operation and set the following session parameter before the CTAS query:

```bash
set session task_writer_count=32
```
{: codeblock}

For details about connecting to a Presto server through a CLI, see [Connecting to a Presto Server](watsonxdata?topic=watsonxdata-con-presto-cli).
{: note}

## Issue: No columns to parse from file error
{: #known_issues25}

When you try to ingest folder from AWS S3 using the ibm-lh tool, the user may get `No columns to parse from file` error, if '0' empty file is in the folder.

**Workaround:** You must first list the folders inside the bucket using `aws s3 ls` command. If '0' empty file is listed, you must copy all the files to another folder using `aws s3 cp` command.
