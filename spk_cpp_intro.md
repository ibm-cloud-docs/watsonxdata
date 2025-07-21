---

copyright:
  years: 2022, 2025
lastupdated: "2025-07-21"

keywords: lakehouse, watsonx.data, Gluten

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

# Introduction to Gluten accelerated Spark engine
{: #prov_cpp_gtn_intr}

Gluten accelerated Spark engine is an optimized, high-performance engine in {{site.data.keyword.lakehouse_short}}. The Spark engine uses Gluten for offloading SQL execution to Velox, which is an open source execution engine(implemented in C++) thereby accelerating the computation of SparkSQL to reduce the cost for running the workloads.

Gluten serves as a native engine plugin designed to accelerate Spark SQL and DataFrame workloads, by integrating native engines with SparkSQL, leveraging the high scalability of the Spark SQL framework and the superior performance of native engines. It is fully compatible with the Apache Spark API, ensuring that no code changes are necessary.


## Features of Gluten accelerated Spark engine
{: #featu_cpp_intr}

* Supports file formats Apache Parquet and Apache Avro.

* Improved table scan performance.

* Accelerates larger SQL queries with joins and aggregation.

* Supports Delta, Hudi, Iceberg and Hive catalogs.

* Faster Delta and Parquet writing using UPDATE, DELETE, MERGE INTO, INSERT, and CREATE TABLE AS SELECT, including wide tables that contain thousands of columns.

* Replaces sort-merge joins with hash-joins by default.

## Limitations
{: #featu_cpp-limt}

* Using Amazon S3 object stores support DAS for application submission, but other object stores like ADLS and GCS requires explicit credentials to be passed.

* Access control is not supported for Gluten engines (Only the user who provision the Gluten engine could access it).


* Smaller queries are not accelerated.
* Catalog association is only supported for s3 object stores.
* Gluten supports only Spark 3.4.


* Fallbacks to JVM

   * ANSI: Gluten currently does not support ANSI mode. If ANSI is enabled, Spark plan's execution will always fall back to vanilla Spark.

   * FileSource format: Currently, Gluten only support Parquet file format and partially support ORC. If other format is used, scan operator falls back to vanilla spark.

* Incompatible behavior

   * JSON functions: Velox only supports double quotes surrounded strings, not single quotes, in JSON data. If single quotes are used, Gluten gives incorrect result.

   * Parquet read configuration: Gluten supports `spark.files.ignoreCorruptFiles` with default false, if true, the behavior is same as config false. Gluten ignores `spark.sql.parquet.datetimeRebaseModeInRead`, it only returns what write in parquet file. It does not consider the difference between legacy hybrid (Julian Gregorian) calendar and Proleptic Gregorian calendar. The result may be different with vanilla spark.

   * Parquet write configuration: Spark has `spark.sql.parquet.datetimeRebaseModeInWrite` config to decide whether legacy hybrid (Julian + Gregorian) calendar or Proleptic Gregorian calendar should be used during parquet writing for dates/timestamps. If the Parquet to read is written by Spark with this config as true, Velox's TableScan will output different result when reading it back.

* Spill

   OutOfMemoryException may still be triggered within current implementation of spill-to-disk feature, when shuffle partitions is set to a large number. When this case happens, please try to reduce the partition number to get rid of the OOM.

* CSV Read

   * The header option should be true. And now we only support DatasourceV1, i.e., user should set spark.sql.sources.useV1SourceList=csv. User defined read option is not supported, which will make CSV read fall back to vanilla Spark in most case. CSV read will also fall back to vanilla Spark and log warning when user specifies schema is different with file schema.

   * For more detailed info on Gluten limitations, see [Limitation](https://github.com/apache/incubator-gluten/blob/main/docs/velox-backend-limitations.md).

* Gluten is not supported for FIPS enabled environment.



## Best Practices for Gluten
{: #featu_cpp-limt_int}


* Gluten requires Large OffHeap memory as integrates with native backend i.e., Velox using Apache Arrow's OffHeap columnar format, which is essential for large-scale data processing without exceeding JVM heap limits.

* If not provided with enough offHeap memory, could lead to potential OOMs (see [Limitation](#featu_cpp-limt)). Therefore, by deault 75% of executor memory is set to offHeap.

* User’s could adjust the percentage of memory set for offHeap, using the configuration, `ae.spark.offHeap.factor`, which accepts values (0-1) exclusive, eg: 0.75.

* It is recommended for users to set this to lower value i.e., < 0.5 if their workload has lot of fallbacks to Java based spark. (see [Limitation](#featu_cpp-limt)) so that OOM does not happen while falling back to Java based spark execution.

* It is recommended to set this to higher value. i.e., 0.75 and above if their workloads executes natively on Gluten without fallback.

By default the value set is 0.75.
