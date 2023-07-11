---

copyright:
  years: 2022, 2023
lastupdated: "2023-07-07"

keywords: watsonxdata, ingesting, object storage bucket, data files, table format. SQL query

subcollection: watsonxdata

content-type: tutorial
account-plan: paid
completion-time: 8h

---

{{site.data.keyword.attribute-definition-list}}


{:step: data-tutorial-type="step"}
{:shortdesc: .shortdesc}

# Ingesting data from object storage bucket
{: #tutorial_ingest_osbckt}
{: toc-content-type="tutorial"}
{: toc-completion-time="8h"}

In this tutorial, you learn to move data into a data lake or an object storage bucket and load the data files to Presto. You will also learn to optimize the file format to choose the table format and run complex SQL query in {{site.data.keyword.lakehouse_full}}.
{: shortdesc}

**Sample Scenario** : You need to run SQL query on data files that is in your object storage bucket. For this, you must attach the data files in your object storage bucket to Presto. You can also convert data into an optimized analytical format in Parquet or ORC to enhance query performance and reduce server and storage resource consumption. Now, you can run SQL query against the table you created.

## Objective
{: #ingest_obj}

* Creating infrastructure within the {{site.data.keyword.lakehouse_short}} service.

* Establishing connection with the customer data bucket.

* Querying from the bucket


## Before you begin
{: #ingest_byb}

This tutorial requires:

* Subscription of {{site.data.keyword.lakehouse_short}} on cloud.
* The configuration details of data bucket that you bring in. This is required for establishing connection with the {{site.data.keyword.lakehouse_short}}.
* Ensure that the data bucket has data.

## Uploading data into an object storage bucket and attaching to Presto
{: #upload_stp1}
{: step}

In this section of the tutorial, you are going to manage data in an object storage bucket and attach the bucket to HMS and associate with Presto engine.
{: shortdesc}

1. Access any one of the object storage access tools like S3 Browser, AWS S3 console, direct S3 APIs, and various CLI/UI object storage tools.
1. Load data files to your object storage bucket by using the tool.
1. Register and attach the object storage bucket to HMS and associate with Presto engine by using {{site.data.keyword.lakehouse_short}} UI.
1. Alternatively, you can also register and attach an object storage bucket with pre-existing data to HMS.

   ORC, Parquet, Avro, RCFile, SequenceFile, JSON, Text (CSV) are the Hive supported file formats.
   {: note}

## Load data files into Presto
{: #load_stp2}
{: step}

After attaching the object storage bucket to HMS, you need to load data files into Presto by creating schema and external tables through the Hive connector.

1. Run the following command to create schema for the data you want to access.

   ```bash
   CREATE SCHEMA <SCHEMA_NAME> WITH ( location = '<SCHEMA_LOCATION>' );
   ```
   {: codeblock}

   For example:
   ```bash
   CREATE SCHEMA hive.gosales WITH ( location = 's3a://lhbeta/gosales' );
   ```
   {: screen}

2. Run the following command to create table by using an external location by pointing to an existing table.

   ```bash
   CREATE TABLE IF NOT EXISTS <TABLE_NAME> ("<COLUMN_NAMES>" <DATA_TYPE>) WITH ( format = '<DATA_FORMAT>', external_location = '<TABLE_LOCATION>' );
   ```
   {: codeblock}

   For example:
   ```bash
   CREATE TABLE IF NOT EXISTS hive.gosales.branch ("BRANCH_CODE" int, "ADDRESS1" varchar, "ADDRESS1_MB" varchar, "ADDRESS2" varchar, "ADDRESS2_MB" varchar, "CITY" varchar, "CITY_MB" varchar, "PROV_STATE" varchar, "PROV_STATE_MB" varchar, "POSTAL_ZONE" varchar, "COUNTRY_CODE" int, "ORGANIZATION_CODE" varchar, "WAREHOUSE_BRANCH_CODE" int) WITH ( format = 'CSV', external_location = 's3a://lhbeta/gosales/branch' );
   ```
   {: screen}

## Generate statistics with analyze table
{: #analyze_stp3}
{: step}

If you want to use the data without creating a new copy for a different table format or more table optimizations, you can generate statistics alone with analyze table.

1. To generate statistics with analyze table, run the following command:

   ```bash
   analyze <TABLE_NAME>;
   ```
   {: codeblock}

   For example:
   ```bash
   analyze hive.gosales.branch;
   ```
   {: screen}

## Convert data to analytics optimized formats (optional)
{: #convert_stp4}
{: step}

You can use the data for creating different table format and more table optimizations. It is recommended to convert the data files to analytics optimized format in Parquet or ORC to improve query performance, reduce server and storage resource consumption. Table format like Iceberg can provide more performance improvements and features like snapshots, time travel, and transactional support for insert, update, and delete.

For example:

1. To create table for a data in CSV format to Parquet format, run `Create table as` command:

   ```bash
   CREATE TABLE IF NOT EXISTS
   <TABLE_NAME>
   WITH ( format = 'PARQUET')
   AS
   SELECT *
   FROM <TABLE_NAME>;
   ```
   {: codeblock}

   ```bash
   CREATE TABLE IF NOT EXISTS
   hive.default.branch
   WITH ( format = 'PARQUET')
   AS
   SELECT *
   FROM hive.gosales.branch;
   ```
   {: screen}

1. To change the table format to Iceberg, run `Create table as` command:

   ```bash
   CREATE TABLE IF NOT EXISTS
   <TABLE_NAME>
   WITH ( format = 'PARQUET')
   AS
   SELECT *
   FROM <TABLE_NAME>;
   ```
   {: codeblock}

   ```bash
   CREATE TABLE IF NOT EXISTS
   iceberg-beta.default.branch
   WITH ( format = 'PARQUET')
   AS
   SELECT *
   FROM hive.gosales.branch;
   ```
   {: screen}

   You can also include any additional SQL into the **SELECT** clause for any transformations or conversion business logic or sort the data for optimized access. You can also add column partitions for additional performance improvements.
   {: note}

   Statistics are automatically generated as part of the ingest of the new table.
   {: note}
