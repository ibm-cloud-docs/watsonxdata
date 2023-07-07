---

copyright:
  years: 2017, 2023
lastupdated: "2023-07-07"

keywords: watsonx.data, spark, table, maintenance
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Getting started with Spark use case
{: #run_samp_file}

This page demonstrates the procedure to run Spark use cases for {{site.data.keyword.lakehouse_short}} by using Python samples. All the samples are written by using Spark Python APIs.

## Prerequisites
{: #spk_preq}

* Provision an {{site.data.keyword.lakehouse_full}} instance.
* Configure an {{site.data.keyword.iae_full_notm}} instance against a {{site.data.keyword.lakehouse_short}} instance.
* Cloud Object Storage bucket connection details.

## About the sample use case
{: #abt_samp_usecase}

The sample file demonstrates the following functionalities:

* Accessing tables from {{site.data.keyword.lakehouse_short}}

    The **Create a database in Lakehouse catalog** section from the [sample python file](#python_file) creates a database **demodb** in the configured {{site.data.keyword.lakehouse_short}} instance with a catalog named **lakehouse**. **demodb** is configured to store all the data and metadata under the Cloud Object Storage(COS) bucket **lakehouse-bucket**. It also creates an iceberg table **testTable** and accesses it.

* Ingesting data to {{site.data.keyword.lakehouse_short}}

    The **Ingest parquet data into a lakehouse table** section from the [sample python file](#python_file) allows you to ingest data in parquet and CSV format from a source Cloud Object Storage bucket **source-bucket** into a {{site.data.keyword.lakehouse_short}} table. Sample data in parquet format is inserted from source COS bucket **source-bucket** into the {{site.data.keyword.lakehouse_short}} table **yellow_taxi_2022**. It also shows ingesting data in CSV format from COS bucket **source-bucket** into the table **zipcode** in the database **demodb**.

    You can download the sample formats from:

    * [Sample parquet file](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page).
    * [Sample CSV file](https://raw.githubusercontent.com/spark-examples/spark-scala-examples/3ea16e4c6c1614609c2bd7ebdffcee01c0fe6017/src/main/resources/zipcodes.csv)

* Modifying schema in {{site.data.keyword.lakehouse_short}}

    The **Schema evolution** section from the [sample python file](#python_file) allows you to modify data in {{site.data.keyword.lakehouse_short}}.

* Performing table maintenance activities in {{site.data.keyword.lakehouse_short}}

    Table maintenance helps in keeping the {{site.data.keyword.lakehouse_short}} table performant. Iceberg provides table maintenance procedures out of the box that allows performing powerful table optimizations in a declarative fashion. The sample below demonstrates how to do some table maintenance operations by using Spark. For more information about the Iceberg Spark table maintenance operations, see [Table Operations](https://iceberg.apache.org/docs/1.2.1/spark-procedures/).

## Running the sample use case
{: #abt_samp_run}

Follow the steps to run the Spark sample python file.

### Spark sample python file
{: #python_file}

```bash

    from pyspark.sql import SparkSession
    import os

    def init_spark():
    spark = SparkSession.builder \
    .appName("lh-hms-cloud") \
    .config("spark.hadoop.fs.s3a.bucket.lakehouse-bucket.endpoint" ,"s3.direct.us-south.cloud-object-storage.appdomain.cloud") \
    .config("spark.hadoop.fs.s3a.bucket.lakehouse-bucket.access.key" ,"<access-key-for-source-bucket>") \
    .config("spark.hadoop.fs.s3a.bucket.lakehouse-bucket.secret.key" ,"<secret-key-for-source-bucket>") \
    .config("spark.hadoop.fs.s3a.bucket.source-bucket.endpoint" ,"s3.direct.us-south.cloud-object-storage.appdomain.cloud") \
    .config("spark.hadoop.fs.s3a.bucket.source-bucket.access.key" ,"<access-key-for-lakehous-bucket>") \
    .config("spark.hadoop.fs.s3a.bucket.source-bucket.secret.key" ,"<secret-key-for-lakehouse-bucket>") \
    .enableHiveSupport() \
    .getOrCreate()

    return spark

    def main():
    try:
        spark = init_spark()
        # Create a database in lakehouse catalog
        spark.sql("create database if not exists lakehouse.demodb LOCATION 's3a://lakehouse-bucket/'")
        # list the database under lakehouse catalog
        spark.sql("show databases from lakehouse").show()

        # demonstration: Create a basic Iceberg table, insert some data and then query table
        spark.sql("create table if not exists lakehouse.demodb.testTable(id INTEGER, name VARCHAR(10), age INTEGER, salary DECIMAL(10, 2)) using iceberg").show()
        spark.sql("insert into lakehouse.demodb.testTable values(1,'Alan',23,3400.00),(2,'Ben',30,5500.00),(3,'Chen',35,6500.00)")
        spark.sql("select * from lakehouse.demodb.testTable").show()

        # demonstration: Ingest parquet and csv data into a wastonx.data Iceberg table
        # load parquet data into dataframce
        df = spark.read.option("header",True).parquet("s3a://source-bucket/nyc-taxi/yellow_tripdata_2022-01.parquet")
        # write the dataframe into an Iceberg table
        df.writeTo("lakehouse.demodb.yellow_taxi_2022").create()
        # describe the table created
        spark.sql('describe table lakehouse.demodb.yellow_taxi_2022').show(25)
        # query the table
        spark.sql('select * from lakehouse.demodb.yellow_taxi_2022').count()

        # load csv data into a dataframe
        csvDF = spark.read.option("header",True).csv("s3a://source-bucket/zipcodes.csv")
        csvDF.createOrReplaceTempView("tempCSVTable")
        # load temporary table into an Iceberg table
        spark.sql('create or replace table lakehouse.demodb.zipcodes using iceberg as select * from tempCSVTable')
        # describe the table created
        spark.sql('describe table lakehouse.demodb.zipcodes').show(25)
        # query the table
        spark.sql('select * from lakehouse.demodb.zipcodes').show()

        # demonstration: Table maintenance
        # load data for the month of Feburary to June into the table yellow_taxi_2022 created above
        df_feb = spark.read.option("header",True).parquet("s3a://source-bucket/nyc-taxi/yellow_tripdata_2022-02.parquet")
        df_march = spark.read.option("header",True).parquet("s3a://source-bucket/nyc-taxi/yellow_tripdata_2022-03.parquet")
        df_april = spark.read.option("header",True).parquet("s3a://source-bucket/nyc-taxi/yellow_tripdata_2022-04.parquet")
        df_may = spark.read.option("header",True).parquet("s3a://source-bucket/nyc-taxi/yellow_tripdata_2022-05.parquet")
        df_june = spark.read.option("header",True).parquet("s3a://source-bucket/nyc-taxi/yellow_tripdata_2022-06.parquet")

        df_q1_q2 = df_feb.union(df_march).union(df_april).union(df_may).union(df_june)
        df_q1_q2.write.insertInto("lakehouse.demodb.yellow_taxi_2022")
        # Query the metadata files table to list underlying data files
        spark.sql("SELECT file_path, file_size_in_bytes FROM lakehouse.demodb.yellow_taxi_2022.files").show()

        # There are many smaller files compact them into files of 200MB each using the
        # `rewrite_data_files` Iceberg Spark procedure
        spark.sql(f"CALL lakehouse.system.rewrite_data_files(table => 'demodb.yellow_taxi_2022', options => map('target-file-size-bytes','209715200'))").show()

        # Query the metadata files table to list underlying data files, 6 files are compacted
        # to 3 files
        spark.sql("SELECT file_path, file_size_in_bytes FROM lakehouse.demodb.yellow_taxi_2022.files").show()

        # Expire earlier snapshots only latest one with comacted data is required
        # list all the snapshots
        spark.sql("SELECT committed_at, snapshot_id, operation FROM lakehouse.demodb.yellow_taxi_2022.snapshots").show()
        #retain only the latest one
        latest_snapshot_committed_at=spark.sql("SELECT committed_at, snapshot_id, operation FROM lakehouse.demodb.yellow_taxi_2022.snapshots").tail(1)[0].committed_at
        print (latest_snapshot_committed_at)
        spark.sql(f"CALL lakehouse.system.expire_snapshots(table => 'demodb.yellow_taxi_2022',older_than => TIMESTAMP '{latest_snapshot_committed_at}',retain_last => 1)").show()

        # Removing Orphan data files
        spark.sql(f"CALL lakehouse.system.remove_orphan_files(table => 'demodb.yellow_taxi_2022')").show(truncate=False)

        # Rewriting Manifest Files
        spark.sql(f"CALL lakehouse.system.rewrite_manifests('demodb.yellow_taxi_2022')").show()

        # demonstration: Schema evolution
        # Add column fare_per_mile to the table
        spark.sql('ALTER TABLE lakehouse.demodb.yellow_taxi_2022 ADD COLUMN(fare_per_mile double)')
        # describe the table
        spark.sql('describe table lakehouse.demodb.yellow_taxi_2022').show(25)
    finally:
        # clean-up the demo database
        spark.sql('drop table if exists lakehouse.demodb.testTable purge')
        spark.sql('drop table if exists lakehouse.demodb.zipcodes purge')
        spark.sql('drop table if exists lakehouse.demodb.yellow_taxi_2022 purge')
        spark.sql('drop database if exists lakehouse.demodb cascade')
        spark.stop()

    if __name__ == '__main__':
    main()
```
{: codeblock}

1. Save the following sample python file.
1. Upload the Python file to the Cloud Object Storage bucket. You must maintain the Spark applications and their dependencies in a Cloud Object Storage bucket and not mix them with data buckets.
1. Generate the IAM token for the {{site.data.keyword.iae_full_notm}} token. For more information about how to generate an IAM token, see [IAM token](https://test.cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-con-presto-thru-cli#get-api-iam-token)
1. Run the following curl command to submit the Spark application:

   ```bash
    curl https://api.<region>.ae.cloud.ibm.com/v3/analytics_engines/<iae-instance-guid>/spark_applications -H "Authorization: Bearer <iam-bearer-token>" -X POST -d '{
    "application_details": {
        "application": "s3a://<application_bucket>/lakehouse-hms-test-cloud-doc-sample.py",
        "conf": {
            "spark.hadoop.fs.s3a.bucket.<application-bucket>.endpoint": "https://s3.direct.us-south.cloud-object-storage.appdomain.cloud",
            "spark.hadoop.fs.s3a.bucket.<application-bucket>.access.key": "<hmac_access_key_for_application-bucket>",
            "spark.hadoop.fs.s3a.bucket.<application-bucket>.secret.key": "<hmac_secret_key_for_application-bucket>"
        }
    }
    }'
   ```
   {: codeblock}


This sample is tested on the Cloud Object Storage buckets in the **us-south** region. Change the region in the Cloud Object Storage endpoint configuration as per the region where your Cloud Object Storage buckets reside. It is recommended to provision the COS buckets in the region where {{site.data.keyword.iae_short}} instance is provisioned.
{: note}
