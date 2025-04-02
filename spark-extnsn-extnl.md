---

copyright:
  years: 2017, 2025
lastupdated: "2025-04-02"

keywords: watsonx.data, spark, emr
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Enhancing Spark application submission using Spark access control extension
{: #spark-extnsn_ext}

When you submit a Spark application that uses external storage buckets registered in {{site.data.keyword.lakehouse_short}}, Spark access control extension allows additional authorization thereby enhancing security. If you enable the extension in the spark configuration, only authorized users are allowed to access and operate {{site.data.keyword.lakehouse_short}} catalogs through Spark jobs.
{: shortdesc}

You can enable the Spark access control extension for Iceberg, Hive and Hudi catalogs.
{: note}



You can either use Ranger or Access Management System (AMS) data policies to grant or deny access for users, user groups, catalog (Iceberg, Hive and Hudi), schema, table, and column. Besides data level authorization, storage privilege is also considered.
For more information related to the using AMS on catalogs(Iceberg, Hive and Hudi), buckets, schemas and tables, see see [Managing roles and privileges](/docs/watsonxdata?topic=watsonxdata-role_priv){: external}.
For more information on how to create Ranger policies (defined under Hadoop SQL service) and to enable them on catalogs(Iceberg, Hive and Hudi), buckets, schemas and tables, see see [Managing Ranger policies](/docs/watsonxdata?topic=watsonxdata-ranger_1){: external}.


## Prerequisites
{: #spk_etnsn_preq-1}

* Create Cloud Object Storage to store data used in the Spark application. To create Cloud Object Storage and a bucket, see [Creating a storage bucket](/docs/watsonxdata?topic=watsonxdata-cos_storage). You can provision two buckets, data-bucket to store {{site.data.keyword.lakehouse_short}} tables and application bucket to maintain Spark application code.
* Register Cloud Object Storage bucket in {{site.data.keyword.lakehouse_short}}. For more information, see [Adding bucket catalog pair](/docs/watsonxdata?topic=watsonxdata-reg_bucket).
* Upload the Spark application to the storage, see [Uploading data](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-upload).
* You must have IAM administrator role or MetastoreAdmin role, for creating schema or table inside {{site.data.keyword.lakehouse_short}}.


## Procedure
{: #spk_extns1}

Spark access control extension supports external Spark engine.

1. To enable the Spark access control extension, you must update the Spark configuration with `add authz.IBMSparkACExtension to spark.sql.extensions`.

2. Save the following Python application as iceberg.py.

Iceberg is considered as an example. You can also use Hive and Hudi catalogs.
{: note}


```bash

from pyspark.sql import SparkSession
import os

def init_spark():
    spark = SparkSession.builder \
        .appName("lh-spark-app") \
        .enableHiveSupport() \
        .getOrCreate()
    return spark

def create_database(spark):
    # Create a database in the lakehouse catalog
    spark.sql("create database if not exists lakehouse.demodb LOCATION 's3a://lakehouse-bucket/'")

def list_databases(spark):
    # list the database under lakehouse catalog
    spark.sql("show databases from lakehouse").show()

def basic_iceberg_table_operations(spark):
    # demonstration: Create a basic Iceberg table, insert some data and then query table
    spark.sql("create table if not exists lakehouse.demodb.testTable(id INTEGER, name VARCHAR(10), age INTEGER, salary DECIMAL(10, 2)) using iceberg").show()
    spark.sql("insert into lakehouse.demodb.testTable values(1,'Alan',23,3400.00),(2,'Ben',30,5500.00),(3,'Chen',35,6500.00)")
    spark.sql("select * from lakehouse.demodb.testTable").show()

def create_table_from_parquet_data(spark):
    # load parquet data into dataframe
    df = spark.read.option("header",True).parquet("file:///spark-vol/yellow_tripdata_2022-01.parquet")
    # write the dataframe into an Iceberg table
    df.writeTo("lakehouse.demodb.yellow_taxi_2022").create()
    # describe the table created
    spark.sql('describe table lakehouse.demodb.yellow_taxi_2022').show(25)
    # query the table
    spark.sql('select * from lakehouse.demodb.yellow_taxi_2022').count()

def ingest_from_csv_temp_table(spark):
    # load csv data into a dataframe
    csvDF = spark.read.option("header",True).csv("file:///spark-vol/zipcodes.csv")
    csvDF.createOrReplaceTempView("tempCSVTable")
    # load temporary table into an Iceberg table
    spark.sql('create or replace table lakehouse.demodb.zipcodes using iceberg as select * from tempCSVTable')
    # describe the table created
    spark.sql('describe table lakehouse.demodb.zipcodes').show(25)
    # query the table
    spark.sql('select * from lakehouse.demodb.zipcodes').show()

def ingest_monthly_data(spark):
    df_feb = spark.read.option("header",True).parquet("file:///spark-vol/yellow_tripdata_2022-02.parquet")
    df_march = spark.read.option("header",True).parquet("file:///spark-vol/yellow_tripdata_2022-03.parquet")
    df_april = spark.read.option("header",True).parquet("file:///spark-vol/yellow_tripdata_2022-04.parquet")
    df_may = spark.read.option("header",True).parquet("file:///spark-vol/yellow_tripdata_2022-05.parquet")
    df_june = spark.read.option("header",True).parquet("file:///spark-vol/yellow_tripdata_2022-06.parquet")
    df_q1_q2 = df_feb.union(df_march).union(df_april).union(df_may).union(df_june)
    df_q1_q2.write.insertInto("lakehouse.demodb.yellow_taxi_2022")

def perform_table_maintenance_operations(spark):
    # Query the metadata files table to list underlying data files
    spark.sql("SELECT file_path, file_size_in_bytes FROM lakehouse.demodb.yellow_taxi_2022.files").show()
    # There are many smaller files compact them into files of 200MB each using the
    # `rewrite_data_files` Iceberg Spark procedure
    spark.sql(f"CALL lakehouse.system.rewrite_data_files(table => 'demodb.yellow_taxi_2022', options => map('target-file-size-bytes','209715200'))").show()
    # Again, query the metadata files table to list underlying data files; 6 files are compacted
    # to 3 files
    spark.sql("SELECT file_path, file_size_in_bytes FROM lakehouse.demodb.yellow_taxi_2022.files").show()
    # List all the snapshots
    # Expire earlier snapshots. Only latest one with compacted data is required
    # Again, List all the snapshots to see only 1 left
    spark.sql("SELECT committed_at, snapshot_id, operation FROM lakehouse.demodb.yellow_taxi_2022.snapshots").show()
    #retain only the latest one
    latest_snapshot_committed_at = spark.sql("SELECT committed_at, snapshot_id, operation FROM lakehouse.demodb.yellow_taxi_2022.snapshots").tail(1)[0].committed_at
    print (latest_snapshot_committed_at)
    spark.sql(f"CALL lakehouse.system.expire_snapshots(table => 'demodb.yellow_taxi_2022',older_than => TIMESTAMP '{latest_snapshot_committed_at}',retain_last => 1)").show()
    spark.sql("SELECT committed_at, snapshot_id, operation FROM lakehouse.demodb.yellow_taxi_2022.snapshots").show()
    # Removing Orphan data files
    spark.sql(f"CALL lakehouse.system.remove_orphan_files(table => 'demodb.yellow_taxi_2022')").show(truncate=False)
    # Rewriting Manifest Files
    spark.sql(f"CALL lakehouse.system.rewrite_manifests('demodb.yellow_taxi_2022')").show()

def evolve_schema(spark):
    # demonstration: Schema evolution
    # Add column fare_per_mile to the table
    spark.sql('ALTER TABLE lakehouse.demodb.yellow_taxi_2022 ADD COLUMN(fare_per_mile double)')
    # describe the table
    spark.sql('describe table lakehouse.demodb.yellow_taxi_2022').show(25)

def clean_database(spark):
    # clean-up the demo database
    spark.sql('drop table if exists lakehouse.demodb.testTable purge')
    spark.sql('drop table if exists lakehouse.demodb.zipcodes purge')
    spark.sql('drop table if exists lakehouse.demodb.yellow_taxi_2022 purge')
    spark.sql('drop database if exists lakehouse.demodb cascade')

def main():
    try:
        spark = init_spark()
        create_database(spark)
        list_databases(spark)
        basic_iceberg_table_operations(spark)
        # demonstration: Ingest parquet and csv data into a watsonx.data Iceberg table
        create_table_from_parquet_data(spark)
        ingest_from_csv_temp_table(spark)
        # load data for the month of February to June into the table yellow_taxi_2022 created above
        ingest_monthly_data(spark)
        # demonstration: Table maintenance
        perform_table_maintenance_operations(spark)
        # demonstration: Schema evolution
        evolve_schema(spark)
    finally:
        # clean-up the demo database
        clean_database(spark)
        spark.stop()

if __name__ == '__main__':
main()

```
{: codeblock}



3. To submit the Spark application, specify the parameter values and run the following curl command. The following example shows the command to submit iceberg.py application.

```bash

curl --request POST   --url https://<region>/lakehouse/api/v2/spark_engines/<spark_engine_id>/applications    --header 'Authorization: Bearer <token>'   --header 'Content-Type: application/json'   --header 'Lhinstanceid: <instance_id>'   --data '{
  "application_details": {
  "conf": {
      "spark.hadoop.fs.s3a.bucket.<wxd-data-bucket-name>.endpoint": "<wxd-data-bucket-endpoint>",
      "spark.hadoop.fs.cos.<COS_SERVICE_NAME>.endpoint": "<COS_ENDPOINT>",
      "spark.hadoop.fs.cos.<COS_SERVICE_NAME>.secret.key": "<COS_SECRET_KEY>",
      "spark.hadoop.fs.cos.<COS_SERVICE_NAME>.access.key": "<COS_ACCESS_KEY>"
      "spark.sql.catalogImplementation": "hive",
      "spark.sql.iceberg.vectorization.enabled":"false",
        "spark.sql.catalog.<wxd-bucket-catalog-name>":"org.apache.iceberg.spark.SparkCatalog",
      "spark.sql.catalog.<wxd-bucket-catalog-name>.type":"hive",
      "spark.sql.catalog.<wxd-bucket-catalog-name>.uri":"thrift://<wxd-catalog-metastore-host>",
      "spark.hive.metastore.client.auth.mode":"PLAIN",
      "spark.hive.metastore.client.plain.username":"<username>",
      "spark.hive.metastore.client.plain.password":"xxx",
      "spark.hive.metastore.use.SSL":"true",
      "spark.hive.metastore.truststore.type":"JKS",
      "spark.hive.metastore.truststore.path":"<truststore_path>",
      "spark.hive.metastore.truststore.password":"changeit",
        "spark.hadoop.fs.s3a.bucket.<wxd-data-bucket-name>.aws.credentials.provider":"com.ibm.iae.s3.credentialprovider.WatsonxCredentialsProvider",
        "spark.hadoop.fs.s3a.bucket.<wxd-data-bucket-name>.custom.signers":"WatsonxAWSV4Signer:com.ibm.iae.s3.credentialprovider.WatsonxAWSV4Signer",
        "spark.hadoop.fs.s3a.bucket.<wxd-data-bucket-name>.s3.signing-algorithm":"WatsonxAWSV4Signer",
        "spark.hadoop.wxd.cas.endpoint":"<cas_endpoint>/cas/v1/signature",
        "spark.hadoop.wxd.instanceId":"<instance_crn>",
        "spark.hadoop.wxd.apikey":"Basic xxx",
        "spark.wxd.api.endpoint":"<wxd-endpoint>",
        "spark.driver.extraClassPath":"opt/ibm/connectors/wxd/spark-authz/cpg-client-1.0-jar-with-dependencies.jar:/opt/ibm/connectors/wxd/spark-authz/ibmsparkacextension_2.12-1.0.jar",
        "spark.sql.extensions":"<required-storage-support-extension>,authz.IBMSparkACExtension"

    },
    "application": "cos://<BUCKET_NAME>.<COS_SERVICE_NAME>/<python_file_name>",
  }
}

```
{: codeblock}

Parameter values:

* `<region>` : Region where the instance is provisioned. Example, `us-south` region.
* `<spark_engine_id>` : The unique identifier of the Spark instance. For information on how to retrieve the ID, see [Managing the Spark engine details](/docs/watsonxdata?topic=watsonxdata-view-end#view-dtls).
* `<token>` : To get the access token for your service instance. For more information about generating the token, see [Generating a token](/docs/watsonxdata?topic=watsonxdata-con-presto-serv#get-ibmiam-token).
* `<instance_id>` : The instance ID from the watsonx.data cluster instance URL. Example, crn:v1:staging:public:lakehouse:us-south:a/7bb9e380dc0c4bc284592b97d5095d3c:5b602d6a-847a-469d-bece-0a29124588c0::.
* `<wxd-data-bucket-name>` : The name of the data bucket associated against the spark engine from the Infrastructure manager.
* `<wxd-data-bucket-endpoint>`: The host name of the endpoint for accessing the data bucket mentioned above. Example, s3.us-south.cloud-object-storage.appdomain.cloud for a Cloud Object storage bucket in us-south region.
* `<wxd-bucket-catalog-name>`: The name of the catalog associated with the data bucket.
* `<wxd-catalog-metastore-host>`: The metastore associated with the registered bucket.
* `<cos_bucket_endpoint>` : Provide the Metastore host value. For more information, see [storage details](/docs/watsonxdata?topic=watsonxdata-run_samp_file#insert_samp_usecase).
* `<access_key>` : Provide the access_key_id. For more information, see [storage details](/docs/watsonxdata?topic=watsonxdata-run_samp_file#insert_samp_usecase).
* `<secret_key>` : Provide the secret_access_key. For more information, see [storage details](/docs/watsonxdata?topic=watsonxdata-run_samp_file#insert_samp_usecase).
* `<truststore_path>`  : Provide the COS path where the trustore certificate is uploaded. For example `cos://di-bucket.di-test/1902xx-truststore.jks`. For more information about generating the trustore, see [Importing self-signed certificates](https://www.ibm.com/docs/en/watsonx/watsonxdata/2.0.x?topic=administering-importing-hms-self-signed-certificates-java-truststore).
* `<cas_endpoint>` : The Data Access Service (DAS) endpoint. To get the DAS endpoint, see [Getting DAS endpoint](/docs/watsonxdata?topic=watsonxdata-cas_ep_ov).
* `<username>` : The username for your watsonx.data instance. Here, ibmlhapikey.
* `<apikey>` : The base64 encoded `ibmlhapikey_<user_id>:<IAM_APIKEY>. Here, <user_id> is the IBM Cloud id of the user whose apikey is used to access the data bucket. To generate API key, log in into the watsonx.data console and navigate to Profile > Profile and Settings > API Keys and generate a new API key.
* `<OBJECT_NAME>`: The IBM Cloud Object Storage name.
* `<BUCKET_NAME>`: The storage bucket where the application file resides.
* `<COS_SERVICE_NAME>`: The Cloud object Storage service name.
* `<python file name>` : The Spark application file name.

Limitations:
* The user must have full access to create schema and table.
* To create data policy, you must associate the catalog to Presto engine.
* If you try to display schema that is not existing, the system throws nullpointer issue.
* You can enable the Spark access control extension for Iceberg, Hive and Hudi catalogs.
