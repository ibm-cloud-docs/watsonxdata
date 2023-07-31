---

copyright:
  years: 2017, 2023
lastupdated: "2023-07-18"

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
        "hms_url": "thrift://XX.XX.XX.XX:9083",
        "hms_auth_type": "PLAIN",
        "hms_username": "test",
        "hms_password": "password",
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
   {: caption="Table 1. IAE configurations" caption-side="bottom"}




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
   {: caption="Table 2. Iceberg configurations" caption-side="bottom"}




   **{{site.data.keyword.lakehouse_short}} configurations**

    | Field | Description |
    |--------------------------|----------------|
    | hms_URL| Specify the HMS URL.|
    | hms_auth_type| Specify the HMS authentication type (default: “PLAIN”).|
    | hms_username| Specify the HMS username.|
    | hms_password| Specify the HMS Password.|
    | lh_endpoint_url| Specify the Cloud Object Storage Endpoint URL.|
    | lh_access_key| Specify the Cloud Object Storage Access Key.|
    | lh_secret_key| Specify the Cloud Object Storage Secret.|
    | app_URL| Specify the Spark Submit Job URL on Cloud Object Storage.|
    {: caption="Table 3. {{site.data.keyword.lakehouse_short}} configurations" caption-side="bottom"}


1. Run the following command to start a Spark procedure that performs the table operations (specified in config.json file) on Iceberg table. Provide the config.json file path as the `file-name`.

    ```bash
    ./ibm-lh table-maint --file <file-name>
    ```
   {: codeblock}

For more information about the `ibm-lh tool` table maintenance utility, see [Table maintenance](https://www.ibm.com/docs/en/watsonxdata/1.0.x?topic=utility-lh-commands-usage#ibm_lh_commands__tablemaint__title__1){: external}.
