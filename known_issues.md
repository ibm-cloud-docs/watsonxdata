---

copyright:
  years: 2022, 2023
lastupdated: "2023-10-11"

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

## Issue: Data ingestion through CLI
{: #known_issues10}

Following are the limitations when ingesting data through the CLI:
* Schema evolution is not supported.
* Partitioning is not supported.
* Iceberg target table is the only supported output format.
* Source CSV file containing TAB or space as delimiter is not supported.
* `pathStyleAccess` property for object storage is not supported.
* Source files must be of the same format type and only Parquet and csv file formats are supported.

## Issue: Data ingestion through web console
{: #known_issues11}

Following are the limitations when ingesting data through the web console:
* Iceberg target table is the only supported format.
* Partitioning is not supported.
* Source CSV file containing TAB or space as delimiter is not supported.
* Configure options are disabled for GA.
* Target table output format is Iceberg and the target data format is Parquet.
* Target storage path is default and cannot be changed.

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

## Issue: Define class error and Name or service not known
{: #known_issues16}

When you restart the Presto engine, the following error is displayed:
`com.googlecode.aviator.exception.CompileExpressionErrorException`.
This error is displayed only once and for the first action that you perform after the engine restart.

**Workaround:** If you see any of the define class error or name or service not known errors, wait for a few minutes for the server to completely restart. Then, retry the query for successful execution.

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

## Issue: Creating the database of type Memory gives an error
{: #known_issues20}

Creating a database of the type Memory gives an error `pq: invalid input syntax for type integer: ""`.

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

When you try to ingest folder from AWS S3 using the **ibm-lh** tool, the following error may be encountered if there are no empty files in the folder:

```bash
No columns to parse from file
```
{: screen}

**Workaround:** First list the folders inside the bucket by using `aws s3 ls` command. If no empty files are listed, copy all the files to another folder by using `aws s3 cp` command.

## Issue: A persistent java.lang.NullPointerException error occurs
{: #known_issues26}

When you run complex and concurrent SQL query workloads, a persistent `java.lang.NullPointerException, 500: Internal Server Error` error occurs in one of the Presto workers as follows:

```bash
2023-08-30T22:12:20.741Z        ERROR   remote-task-callback-3095       com.facebook.presto.execution.StageExecutionStateMachine        Stage execution 20230830_221206_31201_z3xuz.14.0 failed
com.facebook.presto.spi.PrestoException: Expected response code from https://172-17-151-136.fd034d239041414591df37bc2533573e.pod.cluster.local:8480/v1/task/20230830_221206_31201_z3xuz.14.0.5?summarize to be 200, but was 500: Internal Server Error
java.lang.NullPointerException
        at io.airlift.units.Duration.millisPerTimeUnit(Duration.java:237)
        at io.airlift.units.Duration.getValue(Duration.java:94)
        at io.airlift.units.Duration.convertTo(Duration.java:109)
        ....
```
{: screen}

**Workaround:** Pause and resume the engine to restart all worker nodes.
