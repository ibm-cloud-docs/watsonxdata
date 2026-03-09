---

copyright:
  years: 2022, 2025
lastupdated: "2026-02-16"

keywords: watsonx.data, data ingestion, source file

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

# Submitting Spark jobs to migrate Delta Lake tables to Apache Iceberg
{: #migrate_ic_del}

You can use a Spark application to migrate your Delta Lake tables to Apache Iceberg in watsonx.data.
{: shortdesc}


The job converts Delta metadata to Iceberg format while preserving your table structure and optionally maintaining your full snapshot history. You can run the migration for a single table or submit a batch job that migrates multiple tables in one execution.
The job does not rewrite data files, allowing you to migrate tables faster and with reduced resource usage.

## Before you begin
{: #migrate_bfb}

Ensure that the following prerequisites are met:

You have access to the Delta Lake table location.
You have the appropriate permissions to create or register tables in the target Iceberg catalog.
You have the Spark application JAR installed at:
/opt/ibm/spark/builtin-apps/iceberg/iceberg-apps.jar
You know the catalog, schema, and destination table name for the Iceberg table.
Optional: You created a JSON file to run batch migration jobs.


## Migrating a single Delta Lake table to Iceberg
{: #migrate_ic_del}

You can migrate a single Delta Lake table by submitting a Spark job with the required parameters.


Submit a Spark job with the following payload. Specify the Delta table location, Iceberg catalog, schema, and table name.


   ```bash
   {
     "application_details": {
       "application": "/opt/ibm/spark/builtin-apps/iceberg/iceberg-apps.jar",
       "class": "com.ibm.iceberg.apps.DeltaIcebergMigration",
       "arguments": [
         "--delta_table_location", "<path-to-delta-table>",
         "--catalog", "<iceberg_catalog_name>",
         "--schema", "<iceberg_schema_name>",
         "--table", "<iceberg_table_name>"
       ],
       "conf": {
         "ae.spark.driver.log.level": "INFO",
         "ae.spark.executor.log.level": "INFO",
         "spark.hadoop.wxd.apikey": "***"
       }
     }
   }
   ```
   {: codeblock}

Parameter values:


   * `<path-to-delta-table>` : Delta Lake table location path.

   * `<iceberg_catalog_name>` : Iceberg catalog name.

   * `<iceberg_schema_name>` : Iceberg schema or database name.

   * `<iceberg_table_name>` : Iceberg table name.

   * `iceberg_table_location` (Optional) : Iceberg table location path.

   * `table_property` (Optional) : Iceberg table property in key=value format; can be specified multiple times.

   * `latest_snapshot_only` (Optional) : Migrate only the latest snapshot instead of full history (values: true or fase).


## Migrating multiple Delta Lake tables to Iceberg
{: #migrate_ic_del}

You can migrate multiple Delta Lake tables in a single Spark job by providing a migration JSON file.

Create a JSON file that lists all the Delta tables you want to migrate. Include catalog, schema, and table names for each destination Iceberg table.Submit a Spark job and pass the JSON file to the --migration_json argument.

In batch mode, you specify all table‑specific details—such as catalog, schema, table name, and table locations—directly in the migration JSON file.
The --table_property argument applies the same table property to every table that you migrate in the batch.
The icebergTableLocation field is optional in the JSON file. If you exclude it, the utility uses the Delta Lake table location as the Iceberg table location.



Example application Payload:


   ```bash
   {
     "application_details": {
       "application": "/opt/ibm/spark/builtin-apps/iceberg/iceberg-apps.jar",
       "class": "com.ibm.iceberg.apps.DeltaIcebergMigration",
       "arguments": [
         "--migration_json", "<path-to-migration-json>"
       ],
       "conf": {
         "ae.spark.driver.log.level": "INFO",
         "ae.spark.executor.log.level": "INFO",
         "spark.hadoop.wxd.apikey": "***"
       }
     }
   }
   ```
   {: codeblock}

Parameter values:

   * migration_json : JSON configuration file path or inline JSON that defines the batch of tables to migrate.
   * table_property : Iceberg table property in key=value format; applies to all tables in the batch and can be specified multiple times.
   * parallelism : Number of tables to migrate in parallel.
   * latest_snapshot_only : Migrates only the latest snapshot instead of the full snapshot history (true or false).

Example migration JSON:


   ```bash
   {
     "migrations": [
       {
         "deltaTableLocation": "<path-to-delta-table>",
         "icebergTableLocation": "<path-to-iceberg-table>",
         "catalog": "<iceberg_catalog_name>",
         "schema": "<iceberg_schema_name>",
         "table": "<iceberg_table_name>"
       },
       {
         "deltaTableLocation": "<path-to-another-delta-table>",
         "catalog": "<iceberg_catalog_name>",
         "schema": "<iceberg_schema_name>",
         "table": "<another_iceberg_table_name>"
       }
     ]
   }
   ```
   {: codeblock}

Parameter values:

   * deltaTableLocation : Path to the Delta Lake table.
   * icebergTableLocation : Path for the Iceberg table location. If not provided, defaults to the Delta table location.
   * catalog : Target Iceberg catalog name.
   * schema : Target Iceberg schema or database name.
   * table : Target Iceberg table name.
