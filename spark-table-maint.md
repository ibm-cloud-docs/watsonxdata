---

copyright:
  years: 2017, 2025
lastupdated: "2025-08-26"

keywords: watsonx.data, spark, table, maintenance
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Submitting Spark application by using `IBM cpdctl`
{: #spark-table-maint}


**Applies to** : [Spark engine]{: tag-blue}


You can use IBM Cloud Pak for Data Command Line Interface (IBM `cpdctl`) to submit a Spark application in {{site.data.keyword.lakehouse_short}}. The `sparkjob` utility available in the IBM `cpdctl` allows you to submit, list and get the details of a Spark application.
{: shortdesc}


## Prerequisites
{: #table-spk_preq}

* Provision {{site.data.keyword.lakehouse_full}} instance and add a native Spark engine.
* Download and install IBM cpdctl. For information, see [Installing IBM cpdctl](https://www.ibm.com/docs/SSDZ38_2.1.x/wxd-client/topics/cpdctl-title.html).
* Configure the watsonx.data environment in IBM cpdctl. For information, see [Configure IBM cpdctl](https://www.ibm.com/docs/SSDZ38_2.1.x/wxd-client/topics/cpdctl-title.html).



## Procedure
{: #table-spk_sbmtapp}

This section details the procedure to submit a Spark application.
You can create your own Spark application or use the [sample file](#pth_file) available in this topic as reference. The [sample file](#pth_file) is used to perform [Iceberg table maintenance operations](https://iceberg.apache.org/docs/1.8.0/spark-procedures/) using `sparkjob`.

To automatically perform the table maintenance operation, see [Table maintenance operations](/docs/watsonxdata?topic=watsonxdata-cpdctl_commands_wxdata#cpdctl_commands_tabmaint).
{: note}




1. Save the sample [Python file](#pth_file) to a Cloud Object Storage location. You must save the following details of the storage, which is required at the time of submitting the application.

   You can also provide the path to the file if it is saved in your computer. Specify the local path in the `local-path` field.

   The Python file includes commands for the different table maintenance operations. You can uncomment the required section based on your use case scenario. For the use case that involves catalog and schema, customize the catalog_name, schema_name and table_name in the Python file. Also, to customize and use a different query format for table maintenance operations, see [Iceberg procedures](https://iceberg.apache.org/docs/1.8.0/spark-procedures/).
   {: note}

   You can use Amazon S3A, ADLS and GCS storage for Spark job submission.
   {: note}

   * `<Path>` : The path of the storage where the Spark application is saved.

   You must manually save the Python file to a Cloud Object Storage location before using the `<Path>` variable.
   {: note}


   * `<Bucket_Name>` : The name of the Cloud Object Storage storage where the Spark application resides. This storage must be available in the instance and should be associated with the Spark engine.
   * `<Spark_File_Name>` : The name of the Python file.
   * `<BUCKET_ENDPOINT>` : Public endpoint of the Cloud Object Storage storage containing Spark file.
   * `<BUCKET_ACCESS_KEY>` : Access key of the Cloud Object Storage storage.
   * `<BUCKET_SECRET_KEY>` : Secret Key of the Cloud Object Storage storage.
   * `<SPARK_APP_NAME>` : Name of the Spark application.
   * `<API_KEY>` : Generate the <SaaS_API_Key> (See [Generating the API key]({{site.data.keyword.ref-con-presto-serv-link}})).

3. Use the `Create` command in the sparkjob resource available in IBM `cpdctl` to submit the Spark application. See the [How to use wx-data command --help (-h)] section to understand how to run the `./cpdctl wx-data sparkjob create` command.

4. You can list the Spark applications submitted against a Spark engine by using the list command in the sparkjob resource and also get the status of a Spark application by using the get command in the sparkjob resource.


## Spark sample python file
{: #pth_file}

```bash


# SAAS INSTANCE PYTHON TEMPLATE FOR TABLE MAINTENANCE OPERATIONS


from pyspark.sql import SparkSession

def init_spark():

    spark = SparkSession.builder \
        .appName("Table Maintenance") \
        .config('spark.sql.extensions', 'org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions') \
        .enableHiveSupport() \
        .getOrCreate()

    return spark

def main():

    try:
        spark = init_spark()

        # For all commands related to Iceberg Table Maintenance and their details, visit the link given below:
        # https://iceberg.apache.org/docs/1.8.0/spark-procedures/


        # SNAPSHOT MANAGEMENT --------------------------------------------------------------------------------------------------------------


        # Command to get details of all Snapshots in a table
        # You can run the below command to get the details regarding all the snapshots available in a selected table
        # This command can be run using a Presto Engine to get the list of Snapshots of a Table
        # Command Format
        # SELECT committed_at, snapshot_id, parent_id, operation FROM {catalog_name}.{schema_name}."{table_name}$snapshots" ORDER BY committed_at;
        # Command Example
        # SELECT committed_at, snapshot_id, parent_id, operation FROM iceberg_data.iceberg_schema."iceberg_table$snapshots" ORDER BY committed_at;


        # Rollback to Snapshot
        # Command Format
        # spark.sql("CALL {catalog_name}.system.rollback_to_snapshot('{schema_name}.{table_name}', Snapshot_ID)").show()
        # Command Example
        # spark.sql("CALL iceberg_data.system.rollback_to_snapshot('iceberg_schema.iceberg_table', 6825707396795621602)").show()


        # Rollback to TimeStamp
        # Command Format
        # spark.sql("CALL {catalog_name}.system.rollback_to_timestamp('{schema_name}.{table_name}', TIMESTAMP '{Timestamp_of_Snapshot}')").show()
        # Command Example
        # spark.sql("CALL iceberg_data.system.rollback_to_timestamp('iceberg_schema.iceberg_table', TIMESTAMP '2025-02-28T11:49:51.892Z')").show()


        # Set Current Snapshot
        # Command Format
        # spark.sql("CALL {catalog_name}.system.set_current_snapshot('{schema_name}.{table_name}', {Snapshot_ID})").show()
        # Command Example
        # spark.sql("CALL iceberg_data.system.set_current_snapshot('iceberg_schema.iceberg_table', 8505515598581933984)").show()


        # Cherry Pick Snapshot
        # Command Format
        # spark.sql("CALL {catalog_name}.system.cherrypick_snapshot('{schema_name}.{table_name}', {Snapshot_ID})").show()
        # Command Example
        # spark.sql("CALL iceberg_data.system.cherrypick_snapshot('iceberg_schema.iceberg_table', 7141967805447891098)").show()


        # METADATA MANAGEMENT --------------------------------------------------------------------------------------------------------------


        # Expire Snapshot
        # Command Format
        # spark.sql("CALL {catalog_name}.system.expire_snapshots(table => '{schema_name}.{table_name}', snapshot_ids => ARRAY( {ID1}, {ID2}, ... ))").show()
        # Command Example
        # spark.sql("CALL iceberg_data.system.expire_snapshots(table => 'iceberg_schema.iceberg_table', snapshot_ids => ARRAY(2463746222678678017))").show()


        # Remove Orphan Files ( Only lists the Orphan Files as it is a dry run )
        # Command Format
        # spark.sql("CALL {catalog_name}.system.remove_orphan_files(table => '{schema_name}.{table_name}', dry_run => true)").show()
        # Command Example
        # spark.sql("CALL iceberg_data.system.remove_orphan_files(table => 'iceberg_schema.iceberg_table', dry_run => true)").show()


        # Remove Orphan Files ( in the mentioned folder )
        # Command Format
        # spark.sql("CALL {catalog_name}.system.remove_orphan_files(table => '{schema_name}.{table_name}', location => '{tablelocation}/data')").show()
        # Command Example
        # spark.sql("CALL iceberg_data.system.remove_orphan_files(table => 'iceberg_schema.iceberg_table', location => 's3a://iceberg_bucket/iceberg_schema/iceberg_table/data')").show()


        # Rewrite Data Files ( Default Config )
        # Command Format
        # spark.sql("CALL {catalog_name}.system.rewrite_data_files('{schema_name}.{table_name}')").show()
        # Command Example
        # spark.sql("CALL iceberg_data.system.rewrite_data_files('iceberg_schema.iceberg_table')").show()


        # Rewrite Data Files ( Sorting by id and name )
        # Command Format
        # spark.sql("CALL {catalog_name}.system.rewrite_data_files(table => '{schema_name}.{table_name}', strategy => '{strategy_type}', sort_order => '{sort order for id and name}')").show()
        # Command Example
        # spark.sql("CALL iceberg_data.system.rewrite_data_files(table => 'iceberg_schema.iceberg_table', strategy => 'sort', sort_order => 'id DESC NULLS LAST,name ASC NULLS FIRST')").show()


        # Rewrite Manifests
        # Command Format
        # spark.sql("CALL {catalog_name}.system.rewrite_manifests('{schema_name}.{table_name}')").show()
        # Command Example
        # spark.sql("CALL iceberg_data.system.rewrite_manifests('iceberg_schema.iceberg_table')").show()


        # MIGRATION --------------------------------------------------------------------------------------------------------------


        # Register Table
        # Command Format
        # spark.sql("CALL {catalog_name}.system.register_table( table => '{schema_name}.{new_table_name}', metadata_file => '{path/to/metadata/file.json}')").show()
        # Command Example
        # spark.sql("CALL iceberg_data.system.register_table( table => 'iceberg_schema.iceberg_table_new', metadata_file => 's3a://iceberg_bucket/iceberg_schema/iceberg_table/metadata/00000-ebea9-bb80-4a36-497ed503.metadata.json')").show()

    finally:
        spark.stop()

if __name__ == '__main__':
    main()

```
{: codeblock}
