---

copyright:
  years: 2022, 2025
lastupdated: "2025-05-29"

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

## Reset button does not reset the threshold settings to default settings
{: #known_issue46159}

Clicking the `Reset` button does not reset the thresholds to their default or global settings, instead reverts the changes made since the last save which is similar to the action of `Cancel` button.

**Workaround:** To achieve the desired reset to default settings, manually revert each threshold setting to its required value, then save the changes.

## Absence of column NDV stats in Iceberg tables leads to suboptimal query plans
{: #known_issue26023}

In the current implementation, for Iceberg tables within Presto (Java) and Presto (C++), the column NDV (Number of Distinct Values) statistics are not used when available in MDS. NDVs are important to generating optimal query plans. Without them, there can be significant performance degradation.

**Workaround:** For non-partitioned tables, use `SET SESSION <iceberg_catalog>.hive_statistics_merge_strategy='USE_NULLS_FRACTION_AND_NDV';`.

This workaround does not apply to partitioned tables.
{: note}

## `Ingest data` button inoperative in empty table's data sample tab
{: #known_issue44321}

The `Ingest data` button located within the `Data sample` tab of an empty table that is accessible via the Data manager page is currently not functioning as expected. Clicking this button does not initiate the data ingestion process.

**Workaround:** To ingest data into an empty table, please use the Ingest data button available on the main Data manager home page.

## Virtual private network configuration limitation
{: #issue24487}

Private endpoints are not supported for external engines such as IBM Db2 Warehouse, IBM Netezza, and IBM Analytics Engine (Spark).




## HDFS bucket addition is not supported via CPDCTL
{: #known_issue24053}

Adding HDFS buckets is currently not supported by the cpdctl wx-data plugin.

## IBM {{site.data.keyword.lakehouse_short}} Presto connector in Software Hub 5.1.1 and later cannot connect to IBM {{site.data.keyword.lakehouse_short}} Cloud instance
{: #known_issue23411}

IBM {{site.data.keyword.lakehouse_short}} Presto connector fails to connect to IBM {{site.data.keyword.lakehouse_short}} instance due to a 520 Cloudflare error. This issue occurs when multiple simultaneous calls are made to the GET `/engines` API, especially when the {{site.data.keyword.lakehouse_short}} instance has a large number of policies.

## Modifying credentials of the Spark engine home bucket can disrupt data and operations
{: #known_issue24323_22256}

Updating the access credentials for a storage bucket that has been designated as the Spark engine's home bucket during the provisioning process can lead to data access problems and operational failures.

## Metastore admins and metastore viewers are unable to view the schema and table details
{: #known_issue21467}

A user with the metastore admin and metastore viewer privileges in the Query workspace and Data manager, cannot view the schema and table details unless a view policy is defined for schemas and tables.

## Schema evolution scenarios fail in Presto (C++)
{: #known_issue19897}

When you drop and/or add table columns, queries might fail. For example, see the sequence of statements below, after which the queries on the table fail.

   ```bash
      create table ice.s3.tessch.12 (age int, name varchar(25), place varchar(25)
      insert into ice.s3.tessch.t12 values (35, 'ken', 'paris')
      alter table ice.s3.tessch.t12 drop column age
      select * from ice.s3.tessch.t12
      alter table ice.s3.tessch.t8 add column place varchar(25)
   ```
   {: codeblock}

**Workaround:**  For `PARQUET`, run the following command in session:
   ```bash
      set session <catalog-name>.parquet_use_column_names=true;
   ```
   {: codeblock}

Replace `<catalog-name>` with the actual catalog being used.
{: note}

Or set `hive.parquet.use-column-names=true` in catalog properties. For `ORC`, set `hive.orc.use-column-names=true` in catalog properties.

## `Connection Information` page shows a truncated username
{: #known_issue23612}

The `Connection Information` page shows a truncated username, excluding the prefix `ibmlhapikey_` for `PowerBI` and `Looker`.

**Workaround:** Add the `ibmlhapikey_` prefix to the username when manually copying the value to enable connections with BI tools.

## Issue with uppercase Turkish character İ in Oracle database using WE8ISO8859P9 character set (ORA-00911 Error)
{: #known_issue23728}

In an Oracle database using the WE8ISO8859P9 character set, the uppercase Turkish character İ is not supported in the mixed-case feature flag OFF (default) mode, leading to ORA-00911: invalid character errors.

**Workaround:** Set the mixed-case feature flag to ON.

## The default `information_schema` view of a catalog lists schemas and tables from other catalogs
{: #known_issue21054}

If a user has more than one catalog, the default `information_schema` view will display the schemas and tables from other catalogs as well, regardless of the catalogs associated with the engine.

## Hive external column names with uppercase full-width letters cannot be recognized when file-column-names-read-as-lower-case is set to true
{: #known_issue40767}

When the presto worker catalog property file-column-names-read-as-lower-case is set to true, it converts field names in ASCII uppercase letters to ASCII lowercase. As a result, data under column names with uppercase full-width characters will not be recognized and will appear as "null".

## Certificate update required for data ingestion
{: #known_issue40771}

If you encounter issues with Data Source connections in Ingestion discovery, review the certificate details, as the current error message is unclear. A missing/expired certificate is likely causing the issue.

**Workaround:** You must maintain an updated security certificates in order to do ingestion.

## Spark job failure due to expired ADLS signature during Write/Delete/Update operation
{: #known_issue20172}

The Spark job fails with the following error when it performs Write/Delete/Update operation in a ADLS Gen1 storage. This occurs because the ADLS signature expires in the middle of the process.
`java.io.IOException: Server failed to authenticate the request. Make sure the value of Authorization header is formed correctly including the signature`

**Workaround:** Set the ADLS signature expire time to a large value. Configure the property, `spark.hadoop.spark.hadoop.wxd.cas.sas.expiry.period` to control the ADLS signature expire time. Update the default value from 300s to 43200s.

## Presto CLI password size limitation
{: #known_issue15759}

Presto CLI supports a maximum password size of 1 KB (1024 bytes). If the password exceeds this size, the system cannot accept it in the password field; instead, it must be exported.

## The timestamptz datatype is not supported for an ORC table during the upgrade of {{site.data.keyword.lakehouse_short}} web console
{: #known_issue22118}

## Database names containing hyphens or spaces cannot be queried by the Spark engine in a Python notebook, even when the appropriate Spark access control extension has been added.
{: #known_issue38611}

##  Business terms remain after the semantic automation layer integration is deleted from IBM {{site.data.keyword.lakehouse_short}}
{: #known_issues39470}

Business terms that were imported to IBM Knowledge Catalog for a semantic automation layer (SAL) integration in {{site.data.keyword.lakehouse_short}} are not removed when the integration is deleted. This can result in duplicate business terms if a new SAL integration is subsequently enabled and the same or similar business terms are uploaded again.

**Workaround:** To avoid duplicate business terms, the cluster administrator or the user who originally created the SAL registration must manually delete all business terms that were imported for the SAL integration.

## EXISTS clause on Apache Phoenix tables generate Exeception while executing query error
{: #known_issues18858}

Queries involving the EXISTS clause on Apache Phoenix tables may fail unexpectedly, even when the referenced column is valid. This occurs due to limitations in Apache Phoenix's interpretation of the EXISTS clause, particularly in cases with ambiguous or misaligned query structures.

**Workaround:** To address this limitation, apply one of the following strategies:

   - Establish a clear relationship between the subquery and the main query. Introduce a filter condition within the subquery to create a meaningful relationship between the subquery and the main query. For example, where department_id_bigint IS NOT NULL in the subquery. For more information, refer the following example:

      ```bash
      SELECT DISTINCT t1.first_name_varchar, t2.performance_rating_real, t1.team_head_varchar
      FROM phoenix.tm_lh_engine.employee t1, phoenix.tm_lh_engine.departments t2
      WHERE EXISTS (
         SELECT 1
         FROM phoenix.tm_lh_engine.departments
         WHERE department_id_bigint IS NOT NULL
      )
      ```
      {: codeblock}

   - Establish a clear relationship between the tables involved by explicitly joining the tables in the subquery. This ensures the subquery is contextually relevant and resolves the execution issue. For example, where t3.department_id_bigint = t2.department_id_bigint in the subquery. For more information, refer the following example:

      ```bash
      SELECT DISTINCT t1.first_name_varchar, t2.performance_rating_real, t1.team_head_varchar
      FROM phoenix.tm_lh_engine.employee t1, phoenix.tm_lh_engine.departments t2
      WHERE EXISTS (
         SELECT 1
         FROM phoenix.tm_lh_engine.departments t3
         WHERE t3.department_id_bigint = t2.department_id_bigint
      )
      ```
      {: codeblock}

## Hive catalog does not support CSV format for create table int type column
{: #known_issues18049}

The Hive catalog does not support CSV format for create table int type column. The following error is displayed:

   ```bash
   presto> create table  hive_data.hive_schema.intcsv ( type int ) with ( format = 'CSV' ) ;
   Query 20241017_021409_00059_fmcyt failed: Hive CSV storage format only supports VARCHAR (unbounded). Unsupported columns: type integer
   ```
   {: codeblock}

**Workaround**: Use the following options for Hive catalog:

* Create table in varchar.
* Create view that cast the columns to their original data types.

## Inconsistent CSV and Parquet file ingestion behaviour
{: #known_issues26920}

Despite the design specifications stating that CSV files should only be ingested into tables created from CSV files, and parquet files should only be ingested into tables created from parquet files, there is a discrepancy in the actual behaviour where users are able to ingest CSV files into parquet tables. This can result in unexpected results, data quality issues, or performance problems if the schema or formatting of the CSV or parquet file does not align with the expected structure of the target table.

## Invalid file associations in Presto resource group through UI and engine restart issues
{: #known_issues14722}

When an invalid file is associated for an engine in Presto resource group through {{site.data.keyword.lakehouse_short}} UI, the engine will experience a restart. However, the user interface may incorrectly display that the engine is using the newly assigned file.

**Workaround:** If you find that the new file is not associated with {{site.data.keyword.lakehouse_short}} environment, reach out to IBM support for further assistance.

## Time data type support in Hive and Iceberg
{: #known_issues13651}

Hive: The Hive catalog does not natively support the time data type.

Iceberg: Iceberg does support the time data type.

**Workaround:** To enable correct handling of time data in Iceberg tables, the `hive.parquet-batch-read-optimization-enabled` property must be set to `false`.

## Files with different schemas result in null values
{: #known_issues15665}

{{site.data.keyword.lakehouse_short}} now supports ingesting supported file types with varying schemas. However, when columns within these files have distinct schemas, the values in those columns is set to null.

## Unsupported special characters in schema and table creation
{: #known_issues12662}

The following special characters are not supported while creating schemas and tables:

Schemas (Hive and Iceberg): `$`, `^`, `+`, `?`, `*`, `{`, `[`, `(`, `)`, and `/`.

Tables (Hive): `$`, `^`, `+`, `?`, `*`, `{`, `[`, `(`, `)`, and `/`. (Creation of tables within a schema name that starts with the special character `@` shall result in an error).

Tables (Iceberg):`$`, `^`, `+`, `?`, `*`, `{`, `[`, `(`, `)`, `/`, and `@`.

It is recommended to not use special characters such as question mark (?), hyphen (-), asterisk (*) or delimiter characters like \r, \n, and \t in table, column, and schema names. Though these special characters are supported and tables, columns, and schemas can be created, using them might cause issues when running the INSERT command or applying access policies for the same.

To ensure a seamless experience, please follow the list below:
- Schema names can contain letters, numbers or one of `!`, `#`, `&`, `]`, `}`, `<`, `>`, `=`, `%`, and `@`.
- Table names can contain letters, numbers or one of `!`, `#`, `&`, `]`, `}`, `<`, `>`, `=`, and `;`.
- Columns can contain letters, numbers one of `!`, `#`, `&`, `[`, `]`, `<` `>`, `_`, `:`, and `@`.



## `ALTER TABLE` operation fails in Spark job submission
{: #known_issues13596}

Spark jobs that creates a schema, table, and then attempt an `ALTER TABLE` operation may encounter an `authz.AccessControlException` due to insufficient permissions.

This occurs because, even though the schema and table creation are successful, the job tries to execute the `ALTER TABLE` operation before the metastore data is updated with the newly created schema and table details.

**Workaround:** To prevent access denied errors, you must provide a delay in time between each operations that involves creation of new schemas or tables within the same Python script.

**Workaround:** You can disable DAS or make sure that your buckets or object storage are configured with HTTPS endpoints.

## Attempting to read Parquet v2 tables through Presto (C++) results in an error
{: #known_issues12582trial}

When you attempt to read Parquet v2 tables through Presto (C++) that were created via Data manager in {{site.data.keyword.lakehouse_short}}, it gives the following error:

   ```bash
   Error in ZlibDecompressionStream::Next
   ```
   {: codeblock}

**Workaround:** Presto (C++) currently does not support reading Parquet v2 tables. You must copy the data to a new table in v1 format to be compatible for reading using Presto (C++).

1. Set the session property to PARQUET_1_0:

   ```bash
   set session <catalog_name>.parquet_writer_version = 'PARQUET_1_0';
   ```
   {: codeblock}

2. Run the following command to copy the data to a new table:

   ```bash
   create table <catalog name>.<schema name>.<table name> as (select * from <originaltablename>;
   ```
   {: codeblock}

## Spark ingestion currently does not support special characters like quotation marks, back ticks, and parentheses for partitioned table column names.
{: #known_issues12970}

## Attempting to query Query History and Monitoring Management (QHMM) related tables using Presto (C++) engines might encounter errors
{: #known_issues14083}

When you attempt to query QHMM related tables using Presto (C++) engines, you might encounter errors due to unsupported file formats. Presto (C++) supports only Parquet v1 formats. You can not use Presto (C++) to query data or tables in other formats.

**Workaround:** You can switch to use Presto (Java) engines to query QHMM related tables.

## Server concurrency limit reached error in flight server
{: #known_issues13725}

You might encounter a Server concurrency limit reached error when using the flight server to run queries. This occurs when the server experiences high memory usage due to a large number of concurrent requests.

**Workaround:** Increase the number of flight pods or restructure to simplify the queries to reduce the number of sub queries. Adjust the number of replicas based on your system load and available resources.

   Use the following command to scale the number of pods for the `wdp-connect-flight` deployment:

   ```bash
   oc scale deployment wdp-connect-flight --replicas=<number of replicas>
   ```
   {: codeblock}

   For example, if you need to scale the number of pods to 36, run the following command:

   ```bash
   oc scale deployment wdp-connect-flight --replicas=36
   ```
   {: screen}

## Incorrect recognition of Gregorian dates in Presto with Hive Parquet tables
{: #known_issues12050}

Presto exhibits issues when processing historical dates prior to `0200-01-01`, specifically when they are stored in Hive tables formatted as Parquet. This issue occurs due to the conversion between the Gregorian and Julian calendars, which were implemented in `1582-10-15`. Dates before this cutoff date are misinterpreted by Presto.

## Incomplete information on column length in SHOW COLUMNS output
{: #known_issues16248}

The `SHOW COLUMNS` query in Presto currently provides information about columns including name, data type, additional details (extra), and comments. This issue highlights that the existing functionality lacks details about the length of character-based data types (CHAR and VARCHAR). While some connectors return the actual length defined during table creation, others might provide a default value or no information at all.

To address this limitation, three new columns have been added to the `SHOW COLUMNS` output:

* Scale: Applicable to DECIMAL data type, indicating the number of digits after the decimal point.

* Precision: Applicable to numerical data types, specifying the total number of digits. (Default: 10)

* Length: Intended for CHAR and VARCHAR data types, representing the maximum number of characters allowed.

Current Limitations:

* The reported length in the `Length` column might not always reflect the actual size defined in the table schema due to connector limitations.

* Connectors that don't provide length information will display a default value or null depending upon connector.

## Calculation error for OPT_SORTHEAP in Query Optimizer
{: #known_issues11380}

Due to a calculation error in the configuration setting of Query Optimizer for the value of `OPT_SORTHEAP`, the performance of Query Optimizer might be affected.

**Workaround:** To resolve the calculation error for `OPT_SORTHEAP` in Query Optimizer, complete the following steps to update the configuration as `OPT_SORTHEAP= <initial_value>` to `OPT_SORTHEAP <initial_value>/20`.

   1. Set up the `PROJECT_CPD_INSTANCE` environment variable pointing to the namespace where {{site.data.keyword.lakehouse_short}} is installed.

   ```bash
   export PROJECT_CPD_INSTANCE=<wxd_namespace
   ```
   {: codeblock}

   2. Edit the value of `OPT_SORTHEAP` to `OPT_SORTHEAP <initial_value>/20` by running the following command.

   ```bash
   oc edit db2uinstance lakehouse-oaas -n $PROJECT_CPD_INSTANCE
   ```
   {: codeblock}

   3. Wait for sometime for the `STATE` to change to `Ready` for `lakehouse-oaas` and run the following command.

   ```bash
   watch "oc get db2uinstance  -n $PROJECT_CPD_INSTANCE"
   ```
   {: codeblock}

## Limitations - Presto (C++)
{: #known_issues22601_26741}

- Presto (C++) engine currently does not support database catalogs.
- Parquet is the only supported file format.
- Hive connector is supported.
- Default Iceberg table has only read support with Parquet v1 format.
- TPC-H/TPC-DS queries are supported.
- `DELETE FROM` and `CALL SQL` statements are not supported.
- `START`, `COMMIT`, and `ROLLBACK` transactions are not supported.
- Data types `CHAR`, `TIME`, and `TIME WITH TIMEZONE` are not supported. These data types are subsumed by `VARCHAR`, `TIMESTAMP`, and `TIMESTAMP WITH TIMEZONE`.
   - `IPADDRESS`, `IPPREFIX`, `UUID`, `kHYPERLOGLOG`, `P4HYPERLOGLOG`, `QDIGEST`, and `TDIGEST` are not supported.
   - `VARCHAR` supports only a limited length. `Varchar(n)` with a maximum length bound is not supported.
   - `TIME` and `TIME WITH TIMEZONE` is supported in community development.
   - `TIMESTAMP` columns in Parquet files cannot be read.
- Scalar functions:
   - `IPFunctions`, `QDigest`, `HyperLogLog`, and Geospatial internationalization are not supported.
- Aggregate functions:
   - `QDigest`, Classification metrics, and Differential entropy are not supported.
- S3 and S3 compatible file systems (both read and write) are supported.

## Presto (C++) fails to query an external partitioned table
{: #known_issues9897_2}

When you query an external table with `CHAR` data type columns, the query fails to run. This issue occurs due to the limitation that Presto (C++) does not support `CHAR` data types.

**Workaround:** Change the `CHAR` data type column to `VARCHAR` data type.

## Accessing Hive and Iceberg tables in the same glue metastore catalog
{: #known_issues11296}

When using the AWS Glue Data Catalog to manage a bucket or storage location containing both Iceberg and Hive tables, attempting to access Iceberg tables from the Hive catalog gives, `Not a Hive table` error and attempting to access Hive tables from the Iceberg catalog gives, `Not an Iceberg table` error.

## Using ID as a column name in Cassandra `CREATE TABLE`
{: #known_issues12069}

In Cassandra, you cannot create a table with a column named `ID` while using a Cassandra connector through Presto. This is because `ID` is a reserved keyword for the Cassandra driver that is used by Presto, which automatically generates a UUID for each row. Attempting to create a table with a column name ID results in an error message indicating a duplicate column declaration as follows:
Duplicate column `id` declaration for table `tm_lakehouse_engine_ks.testtable12`

**Workaround:** Avoid using `ID` as a column name when creating Cassandra tables through Presto.

## User role with `CreateCollection` L3 policy fails to create collection in Milvus
{: #known_issues12918}

Users with `User role` while creating collections in Milvus with pymilvus can fail when using the `ORM Connection` and `MilvusClient Connection` methods.

**Workaround:** You must follow the instructions:

`ORM Connection`: The user requires both DescribeCollection and CreateCollection privileges granted in the L3 policy page. You must select all collections in a database while granting `DescribeCollection` privilege in the L3 policy through web console.

`MilvusClient Connection`: Only `CreateCollection` privilege is necessary in the L3 policy page. However, the first attempt to create a collection will fail.

   1. Run the `create_collection` function once.
   2. Re-run the `create_collection` function again. This allows the policies to synchronise and the collection creation will succeed.

## Special characters and mixed case impacting data synchronization
{: #known_issues11040}

When synchronizing data between buckets containing tables or schemas with special characters or mixed case letters in their names, you might encounter with the following unexpected behaviors:
- Tables or schemas with certain special characters `%`, `,`, `{`, `)`, `(`, `@`, `$`, `[`, `:` will have their data entirely skipped during synchronization.
- Tables or schemas with mixed case or uppercase letters will be converted to lowercase before synchronization.

**Workaround:** Avoid using special characters and mixed case in table and schema names. Rename existing tables and schemas to use only the supported characters.

## Missing data validation for Amazon S3 storage endpoints
{: #known_issues11921}

Currently, the user interface (UI) does not perform data validation for endpoints associated with the Amazon S3 storage type.

## Incorrect alias usage in `WITH` clause and `USE catalog.schema`
{: #known_issues11278}

`WITH` clause: When referencing data within the `WITH` clause, use the exact alias name assigned during its definition. Using an incorrect alias triggers the following error message.

```bash
Schema must be specified when session schema is not set
```
{: codeblock}

`USE catalog.schema` usage along with `WITH` clause: When tables are specified using `WITH` and `USE catalog.schema`, queries with incorrect alias names will result in the following error.

```bash
Table does not exist
```
{: codeblock}

## String literal interpretation in Presto (Java)
{: #known_issues6042}

Presto (Java), by default interprets string literals as VARCHAR, unlike many other database systems that treat them as CHAR.

In Presto (Java), string comparisons are performed on the actual characters present in the string, excluding trailing spaces. This can cause queries to return incorrect results when working with strings that may contain trailing spaces, as these spaces are not considered during comparison.

## Table names with multiple dots
{: #known_issues9908}

Presto (Java) does not support creating or querying table names that contain three or more consecutive dots in its name. Attempts to reference such tables in queries may result in errors.

## User is still visible in the Access control page of an engine after removing the user from IAM.
{: #known_issues5081}

## LDAP authentication is not supported for Teradata connector.
{: #known_issues11180}

The {{site.data.keyword.lakehouse_short}} Teradata connector does not currently support LDAP (Lightweight Directory Access Protocol) for user authentication.

**Workaround:** If you encounter the 502 error, reload the Spark history UI page after waiting 1-5 seconds. This should allow enough time for the server to become operational.

## Cross catalog schema creation anomaly in Presto.
{: #known_issues8937}

An anomaly exists in schema creation for Hive and Iceberg catalogs managed by Presto. When using a common Hive Metastore Service for multiple catalogs (Example, an Iceberg catalog and a Hive catalog, or two Iceberg or Hive catalogs), creating a schema in one catalog might create it in a wrong catalog. This occurs if the location specified during schema creation belongs to a different catalog than intended.

**Workaround:** You must always explicitly provide the correct storage path associated with the target catalog when using `CREATE SCHEMA` statements in Presto. This ensures the schema is created in the desired location.

## Presto (Java) queries with many columns and size exceeding default limit.
{: #known_issues3177}

Presto (Java) queries involving multiple tables with a large number of columns (for example, 1000 columns per table or more) in the `SELECT` clause might encounter performance issues across all deployment environments.

The iterative optimizer times out when `max_reorder_joins` is set to 5 or higher (the default timeout is 3 minutes) and gives the following error:

```bash
The optimizer exhausted the time limit of 180000 ms
```
{: codeblock}

For queries exceeding the default `max-task-update-size` limit (16MB in Presto (Java)), you might observe a `TaskUpdate size exceeding this limit` error (the specific value of limit depends on the actual query).

**Workaround:**
- You can improve query performance by temporarily disabling the `reorder_joins` rule using the following session property:

   ```bash
   set session reorder_joins = false;
   ```
   {: codeblock}

- Increase the `max-task-update-size` value in the **config.properties** file if the issue involves a `TaskUpdate size exceeding the limit` error and restart Presto (Java).

Example:
   ```bash
   experimental.internal-communication.max-task-update-size=64MB
   ```
   {: codeblock}

## Limitation: Transactions not supported in unlogged Informix databases.
{: #known_issues9782}

In {{site.data.keyword.lakehouse_short}}, when attempting to execute queries with transactional implications on unlogged Informix databases, queries will fail. This is because unlogged Informix databases, by design, do not support transactions.

## Limitation: Netezza Performance Server INSERT statement limitation.
{: #known_issues9230}

Netezza Performance Server currently does not support inserting multiple rows directly into a table using VALUES clause. This functionality is limited to single-row insertions. Refer to the official Netezza Performance Server [documentation](https://www.ibm.com/docs/hr/psfa/7.1.0?topic=reference-insert) for details on the INSERT statement.

The following example using VALUES for multiple rows is not supported:
```bash
INSERT INTO EMPLOYEE VALUES (3,'Roy',45,'IT','CityB'),(2,'Joe',45,'IT','CityC');
```
{: codeblock}

**Workaround:** Use a subquery with SELECT and UNION ALL to construct a temporary result set and insert it into the target table.
```bash
INSERT INTO EMPLOYEE SELECT * FROM(SELECT 4,'Steve',35,'FIN','CityC' UNION ALL SELECT 5,'Paul',37,'OP','CityA') As temp;
```
{: codeblock}

## Issue: Milvus unresponsive to queries.
{: #known_issues9946}

Milvus may not respond to queries when attempting to load collections or partitions that exceed available memory capacity. This occurs because all search and query operations within Milvus are executed in memory, requiring the entire collection or partition to be loaded before querying.

**Workaround:**

* Consider the memory limitations of your Milvus deployment and avoid loading excessively large collections or partitions.

* If Milvus becomes unresponsive to queries, employ the appropriate Milvus API to unload or release some collections from memory. An example using Python SDK: `collection.release()`

## Issue: Inaccurate row count after deletions in Milvus.
{: #known_issues9947}

The `collection.num_entities` property might not reflect the actual number of rows in a Milvus collection after deletion operations. This property provides an estimate and may not account for deleted entities.

To get an accurate count of rows, execute a `count(*)` query on the collection. This provides an accurate count even after deletions.

Pymilvus syntax:
```bash
collection = pymilvus.Collection(...)
collection.query(expr='', fields=['count(*)'])
```
{: codeblock}

## Limitations: Unsupported Db2 operations.
{: #known_issues7895}

{{site.data.keyword.lakehouse_short}} currently does not support the ALTER TABLE DROP COLUMN operation for Db2 column-organized tables.

   By default, Db2 instances create tables in column-organized format.
   {: note}

{{site.data.keyword.lakehouse_short}} does not support creating row-organized tables in Db2.

## Limitations: Handling Null Values in Elasticsearch.
{: #known_issues8294}

**Elasticsearch** connector requires explicit definition of index mappings for fields to handle null values when loading data.

## Limitations: Loading Nested JSON with Elasticsearch.
{: #known_issues8294(2)}

**Elasticsearch** connector requires users to explicitly specify nested JSON structures as arrays of type ROW for proper loading and querying. To process such structures, use the UNNEST operation.

## Limitation: Users can create 3 instances of Milvus service for a single instance of {{site.data.keyword.lakehouse_short}} in IBM Cloud.
{: #known_issues6821}

## Issue: Unable to create views in Presto.
{: #known_issues1.0.0_6}

Presto describes a view in a mapped database as a TABLE rather than a VIEW. This is apparent to JDBC program connecting to the Presto engine.

## Issue: User is not removed from the catalog access control on revoking data access.
{: #known_issues1.0.0_3}

When you grant user access to a user by adding them to the data control policies by using the **Access Control** screen, the user is successfully listed against the catalog. On revoking user access from the **Access Control** page, the user stays listed against the catalog and continues to have user access.

## Issue: Unable to view expected catalogs from Presto (Java).
{: #known_issues1.0.0_2}

Users with administrator privileges are unable to view the expected Hive and PostgreSQL catalogs from Presto (Java).

## Issue: Console UI lists invalid users.
{: #known_issues1.0.0_1}

{{site.data.keyword.lakehouse_short}} user (user1) invites a new user (user2) to the account by using the **Manage access and users** screen (**Manage > Access (IAM) > Manage access and users**) and grants access to a role (MetastoreAccess, Viewer, Operator, Editor, Administrator). User2 gets access to resources in the {{site.data.keyword.lakehouse_short}} instance through user1's account. Additionally, user2 is granted data access at the resource level by adding to the data control policies by using the **Access Control** screen.
When user1 removes user2 from the user1's account, user2 is still listed in the **Access Control** tab at resource level.


## Issue: Unable to view created schema.
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

## Issue: Access denied when querying an external database.
{: #known_issues2}

When a user with the User role and Create access (the user only has Create access), is added to an external database, they cannot run the select query from the table they have created. Though the user can connect to the Presto (Java) engine and create tables and schemas, they cannot query from the table. The system displays a `Access Denied` message.

```bash
Query 20230608_132213_00042_wpmk2 failed: Access Denied: Cannot select from columns [id] in table or view tab_appiduser_01
```
{: codeblock}

**Workaround:** Provide select privilege for the table the user created.

## Issue: Schema created under different catalog.
{: #known_issues5}

Schemas are available across Iceberg and Hive catalogs. When a schema is created under Iceberg catalog, it is listed under Hive catalog and vice versa.

## Issue: Presto (Java) does not support deletion of Iceberg tables.
{: #known_issues6}

## Issue: DROP SCHEMA in Db2.
{: #known_issues7}

In Db2, the schema can be dropped only if it is empty. Initiating `DROP SCHEMA` statement against a non-empty schema may result in Db2 SQL Error `SQLCODE=-478` and `SQLSTATE=42893`.

## Issue: CREATE VIEW statement that is partially supported by Db2.
{: #known_issues8}

Db2 connector partially supports `CREATE VIEW` statement. The Presto (Java) supported SQL syntax does not include creating views with custom column names (different than the table column names).

## Issue: CREATE VIEW statement that is partially supported by {{site.data.keyword.netezza_short}}.
{: #known_issues9}

{{site.data.keyword.netezza_short}} connector partially supports `CREATE VIEW` statement. The Presto (Java) Supported SQL syntax does not include creating views with custom column names (different than the table column names).

## Issue: Presto (Java) does not recognize the path as a directory.
{: #known_issues12}

When you create a new table with a Presto (Java) Hive connector that uses an S3 folder from an external location, Presto (Java) does not recognize the path as a directory and an error might occur.

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

Objects in a file system are stored as objects and their path. The object and path must have an associated metadata. If the path is not associated with the metadata, Presto (Java) fails to recognize the object and responds that the path is not a directory.

## Issue: Assigning Grant or Revoke privilege.
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

## Issue: Creating schema without a location.
{: #known_issues14}

When you create a schema without a location, it is not listed in the schema list of any catalog.
For example, if you create a schema without specifying the location of the bucket, the schema is created in HMS and not in the bucket. When you try to create a new schema with the same name, it fails and responds that the schema already exists.

**Workaround:** Specify the location of the bucket when creating a schema.

## Issue: Unique names for schema and bucket.
{: #known_issues15}

A schema and a bucket cannot be created with the same name.
For example, if you create a schema that is named “sales” in one catalog, the same name cannot be used for another schema in another catalog. Similarly, if you register a bucket with the name “salesbucket”, another bucket with the same cannot be registered, even if the bucket is located in a different object store.

**Workaround:** Use unique names when creating schemas and buckets.

## Issue: Creating schema for target table.
{: #known_issues17}

You must create schema for the target table if the schema does not exist.

## Issue: Ingestion fails if CSV file contains bad record.
{: #known_issues18}

**ibm-lh** tool does not support skipping maximum bad records for CSV files if the mismatch field is greater than the table definition.

## Issue: Creating schema location with path.
{: #known_issues19}

Use one of the following location options when creating a schema:

- Location pointing to a bucket/subpath without a trailing `/`.
- Location pointing to a bucket/subpath with a trailing `/` – Recommended for better structuring.

Though you can use a location pointing to a bucket only with or without a trailing `/`, it might lead to failure. Therefore, it is recommended to use a subpath.
{: note}

## Issue: Presto (Java) do not support `AS OF` with iceberg tables.
{: #known_issues21}

Presto (Java) do not support `AS OF <time stamp>` command in a SELECT query.

**Workaround:** Invoke `CALL iceberg_data_rollback_to_snapshot` to move to the required timestamp.

If you use `CALL iceberg_data_rollback_to_snapshot` with a timestamp, you cannot call the stored procedure to move to a later timestamp. Use Spark SQL as an alternative.
{: note}

## Issue: Only the creator has DROP access on the table in Apache Hive (API).
{: #known_issues22}

Only the creator of a table can drop the table that is created in the Apache Hive catalog. Other users cannot drop the table even if they have an explicit DROP access to the table. They get the `Access Denied` message.

## Issue: User-provided certificates are not supported by {{site.data.keyword.lakehouse_short}}.
{: #known_issues23}

Currently, user-provided certificates are not supported in {{site.data.keyword.lakehouse_short}} when adding database connections, object store buckets, or when using ibm-lh utility.

## Issue: No columns to parse from file error.
{: #known_issues25}

When you try to ingest folder from AWS S3 using the **ibm-lh** tool, the following error may be encountered if there are no empty files in the folder:

```bash
No columns to parse from file
```
{: screen}

**Workaround:** First list the folders inside the bucket by using `aws s3 ls` command. If no empty files are listed, copy all the files to another folder by using `aws s3 cp` command.

## Special characters in target table names can cause ingestion failures.
{: #known_issues30}

Ingestion fails if a target table name contains special characters in it when ingesting through the web console.

**Workaround:** You can ingest data by using ingestion through Spark CLI.

## Limitation: Presto (Java) does not support `VARBINARY` datatype.
{: #known_issues31}

The current version of Presto (Java) does not support binary strings with length. Execution of an `ALTER TABLE` statement on a database results in the following error:

`Unknown type 'varbinary(n)' for column 'testcolumn'`

This is a limitation in Preso and not a limitation in {{site.data.keyword.lakehouse_short}}.
{: note}

## Limitation: Back up your data to prevent data loss while working with VS Code development environment - Spark Labs.
{: #known_issues32}

As Spark labs are ephemeral in nature, you must back up the data stored periodically to prevent potential data loss during upgrades or a Spark master crash.
