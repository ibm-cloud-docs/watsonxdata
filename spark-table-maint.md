---

copyright:
  years: 2017, 2025
lastupdated: "2025-03-05"

keywords: watsonx.data, spark, table, maintenance
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Spark table maintenance by using `ibm-lh` tool
{: #table-run_samp_file}

You can perform Iceberg table maintenance operations by using Spark with the help of `ibm-lh` tool.
This topic provides information about the following {{site.data.keyword.lakehouse_full}} table maintenance operations that can be done by using Spark with the help of`ibm-lh` tool.
{: shortdesc}

* Snapshot management

    - rollback_to_snapshot - Roll back a table to a specific snapshot ID.
    - rollback_to_timestamp - Roll back the table to a snapshot at a specific day and time.
    - set_current_snapshot - Sets the current snapshot ID for a table.
    - cherrypick_snapshot - Cherry-picks changes from a snapshot into the current table state.
* Metadata management
    - expire_snapshots - Remove older snapshots and their files that are no longer needed.
    - remove_orphan_files - Used to remove files that are not referenced in any metadata files of an Iceberg table.
    - rewrite_data_files - Combines small files into larger files to reduce metadata overhead and runtime file open cost.
    - rewrite_manifests - Rewrite manifests for a table to optimize scan planning.
* Table Migration
    - register_table - Creates a catalog entry for a metadata.json file that exists but does not have a corresponding catalog identifier.

For more table operations, see [Spark Procedures](https://iceberg.apache.org/docs/latest/spark-procedures/).


## Prerequisites
{: #table-spk_preq}

* Provision {{site.data.keyword.lakehouse_full}} instance
* Provision {{site.data.keyword.iae_full_notm}} instance
* Install `ibm-lh` tool. For more information on how to install `ibm-lh` tool, see [Installing ibm-lh-client](https://www.ibm.com/docs/en/watsonxdata/1.0.x?topic=package-installing-lh-client){: external}.

## Spark sample python file
{: #pth_file}

    ```bash
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
        # Command Format
        # SELECT committed_at, snapshot_id, parent_id, operation FROM catalog_name.schema_name."table_name$snapshots" ORDER BY committed_at;
        # Command Example
        # SELECT committed_at, snapshot_id, parent_id, operation FROM iceberg_data.iceberg_schema."iceberg_table$snapshots" ORDER BY committed_at;


        # Rollback to Snapshot
        # Command Format
        # spark.sql("CALL catalog_name.system.rollback_to_snapshot('schema_name.table_name', Snapshot_ID)").show()
        # Command Example
        # spark.sql("CALL iceberg_data.system.rollback_to_snapshot('iceberg_schema.iceberg_table', 6825707396795621602)").show()


        # Rollback to TimeStamp
        # Command Format
        # spark.sql("CALL catalog_name.system.rollback_to_timestamp('schema_name.table_name', TIMESTAMP '2021-06-30T00:00:00.000Z')").show()
        # Command Example
        # spark.sql("CALL iceberg_data.system.rollback_to_timestamp('iceberg_schema.iceberg_table', TIMESTAMP '2025-02-28T11:49:51.892Z')").show()


        # Set Current Snapshot
        # Command Format
        # spark.sql("CALL catalog_name.system.set_current_snapshot('schema_name.table_name', Snapshot_ID)").show()
        # Command Example
        # spark.sql("CALL iceberg_data.system.set_current_snapshot('iceberg_schema.iceberg_table', 8505515598581933984)").show()


        # Cherry Pick Snapshot
        # Command Format
        # spark.sql("CALL catalog_name.system.cherrypick_snapshot('schema_name.table_name', Snapshot_ID)").show()
        # Command Example
        # spark.sql("CALL iceberg_data.system.cherrypick_snapshot('iceberg_schema.iceberg_table', 7141967805447891098)").show()


        # METADATA MANAGEMENT --------------------------------------------------------------------------------------------------------------


        # Expire Snapshot
        # Command Format
        # spark.sql("CALL catalog_name.system.expire_snapshots(table => 'schema_name.table_name', snapshot_ids => ARRAY( ID1, ID2, ... ))").show()
        # Command Example
        # spark.sql("CALL iceberg_data.system.expire_snapshots(table => 'iceberg_schema.iceberg_table', snapshot_ids => ARRAY(2463746222678678017))").show()


        # Remove Orphan Files ( Only lists the Orphan Files as it is a dry run )
        # Command Format
        # spark.sql("CALL catalog_name.system.remove_orphan_files(table => 'schema_name.table_name', dry_run => true)").show()
        # Command Example
        # spark.sql("CALL iceberg_data.system.remove_orphan_files(table => 'iceberg_schema.iceberg_table', dry_run => true)").show()


        # Remove Orphan Files ( in the mentioned folder )
        # Command Format
        # spark.sql("CALL catalog_name.system.remove_orphan_files(table => 'schema_name.table_name', location => 'tablelocation/data')").show()
        # Command Example
        # spark.sql("CALL iceberg_data.system.remove_orphan_files(table => 'iceberg_schema.iceberg_table', location => 's3a://iceberg_bucket/iceberg_schema/iceberg_table/data')").show()


        # Rewrite Data Files ( Default Config )
        # Command Format
        # spark.sql("CALL catalog_name.system.rewrite_data_files('schema_name.table_name')").show()
        # Command Example
        # spark.sql("CALL iceberg_data.system.rewrite_data_files('iceberg_schema.iceberg_table')").show()


        # Rewrite Data Files ( Sorting by id and name )
        # Command Format
        # spark.sql("CALL catalog_name.system.rewrite_data_files(table => 'schema_name.table_name', strategy => 'sort', sort_order => 'id DESC NULLS LAST,name ASC NULLS FIRST')").show()
        # Command Example
        # spark.sql("CALL iceberg_data.system.rewrite_data_files(table => 'iceberg_schema.iceberg_table', strategy => 'sort', sort_order => 'id DESC NULLS LAST,name ASC NULLS FIRST')").show()


        # Rewrite Manifests
        # Command Format
        # spark.sql("CALL catalog_name.system.rewrite_manifests('schema_name.table_name')").show()
        # Command Example
        # spark.sql("CALL iceberg_data.system.rewrite_manifests('iceberg_schema.iceberg_table')").show()


        # MIGRATION --------------------------------------------------------------------------------------------------------------


        # Register Table
        # Command Format
        # spark.sql("CALL catalog_name.system.register_table( table => 'schema_name.new_table_name', metadata_file => 'path/to/metadata/file.json')").show()
        # Command Example
        # spark.sql("CALL iceberg_data.system.register_table( table => 'iceberg_schema.iceberg_table_new', metadata_file => 's3a://iceberg_bucket/iceberg_schema/iceberg_table/metadata/00000-ebea9-bb80-4a36-497ed503.metadata.json')").show()

    finally:
        spark.stop()

if __name__ == '__main__':
    main()


    ```
    {: codeblock}



## Procedure
{: #table-abt_samp_run}

Follow the steps to run the Spark sample python file.

1. Save the following config.json file to the root location where you installed `ibm-lh` tool.

    ```bash
    {
    "iae": {
        "iam_api_key": "",
        "iae_endpoint_url": "https://api.us-south.ae.cloud.ibm.com/",
        "api_auth_url": "https://iam.cloud.ibm.com/identity/token",
        "iae_instance_id": "XXX"
    },
    "table": {
        "catalog": "catalog",
        "schema": "db",
        "table_name": "table",
        "table_action": "register_table",
        "snapshot_id": "1",
        "snapshot_timestamp": "2012-10-31:01:00:00.000",
        "snapshot_table": "snapshot_table",
        "spark_catalog": "spark_catalog",
        "metadata_file": "s3a://new-bucket"
    },
    "lakehouse": {
        "mds_url": "thrift://XX.XX.XX.XX:9083",
        "mds_auth_type": "PLAIN",
        "mds_username": "test",
        "mds_password": "password",
        "lh_endpoint_url": "https://s3.us-south.cloud-object-storage.appdomain.cloud",
        "lh_access_key": "",
        "lh_secret_key": "",
        "app_url": "s3a://new-bucket/table-ops-job.py"
    }
    }
    ```
    {: codeblock}

1. Configure the config.json file with the following information.


    **IAE configurations**

    | Field | Description |
    |--------------------------|----------------|
    |iam_api_key| Specify the IBM IAE API Key|
    |iae_endpoint_url| IAE Endpoint URL (https://api.us-south.ae.cloud.ibm.com/).|
    |api_auth_url| IAE Authorization API URL (https://iam.cloud.ibm.com/identity/token).|
    |iae_instance_id| IAE Instance ID.|
   {: caption="IAE configurations" caption-side="bottom"}




   **Iceberg configurations**

    | Field | Description |
    |--------------------------|----------------|
    |catalog| Specify the Iceberg catalog.|
    | schema| Specify the Iceberg schema.|
    | table_name| Specify the Iceberg Table Name.|
    | table_action| Specify the table operations to be performed (Options - expire_snapshots, remove_orphan_files, rewrite_data_files, rewrite_manifests, rollback_to_snapshot, rollback_to_timestamp, set_current_snapshot, cherrypick_snapshot, register_table).|
    | “snapshot_id”: “1"| Specify the Iceberg table snapshot ID.|
    | snapshot_timestamp| Specify the Iceberg table snapshot timestamp (Format-“2012-10-31:01:00:00.000”).|
    | snapshot_table| Specify the Iceberg table snapshot table name.|
    | spark_catalog| Specify the catalog for register_table action.|
    | metadata_file| Specify the metadata path for register_table action.|
   {: caption="Iceberg configurations" caption-side="bottom"}




   **{{site.data.keyword.lakehouse_short}} configurations**

    | Field | Description |
    |--------------------------|----------------|
    | mds_URL| Specify the MDS URL.|
    | mds_auth_type| Specify the MDS authentication type (default: “PLAIN”).|
    | mds_username| Specify the MDS username.|
    | mds_password| Specify the MDS Password.|
    | lh_endpoint_url| Specify the Cloud Object Storage Endpoint URL.|
    | lh_access_key| Specify the Cloud Object Storage Access Key.|
    | lh_secret_key| Specify the Cloud Object Storage Secret.|
    | app_URL| Specify the Spark Submit Job URL on Cloud Object Storage.|
    {: caption="{{site.data.keyword.lakehouse_short}} configurations" caption-side="bottom"}


1. Run the following command to start a Spark procedure that performs the table operations (specified in config.json file) on Iceberg table. Provide the config.json file path as the `file-name`.

    ```bash
    ./ibm-lh table-maint --file <file-name>
    ```
   {: codeblock}

For more information about the `ibm-lh tool` table maintenance utility, see [Table maintenance](https://www.ibm.com/docs/en/watsonxdata/1.0.x?topic=utility-lh-commands-usage#ibm_lh_commands__tablemaint__title__1){: external}.
