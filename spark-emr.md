---

copyright:
  years: 2017, 2024
lastupdated: "2024-01-31"

keywords: watsonx.data, spark, emr
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Using AWS EMR for Spark use case
{: #spark-emr}

The topic provides the procedure to run Spark applications from Amazon Web Services Elastic MapReduce (AWS EMR) to achieve the {{site.data.keyword.lakehouse_full}} Spark use cases:
* data ingestion
* data querying
* table maintenance
{: shortdesc}


## Prerequisites
{: #spk_emr_preq}

* Provision {{site.data.keyword.lakehouse_full}} instance.
* Create a catalog with S3 bucket.
* Get S3 bucket credentials.
* Set up EMR cluster on AWS. For more information, see [Setting up an EMR Cluster](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-setting-up.html).
* Fetch the following information from {{site.data.keyword.lakehouse_full}}:
    * HMS URL from {{site.data.keyword.lakehouse_short}}. For more information about getting the HMS credentials, see [Getting (Hive metastore) HMS Credentials](watsonxdata?topic=watsonxdata-hms){: external}.
    * HMS Credentials from {{site.data.keyword.lakehouse_short}}. For more information about getting the HMS credentials, see [Getting (Hive metastore) HMS Credentials](watsonxdata?topic=watsonxdata-hms){: external}.

## Overview
{: #abt_emr_usecase}

To work with source data that resides in AWS S3 buckets, you can do either of the following ways:
* setup {{site.data.keyword.lakehouse_short}} instance on AWS
* configure IBM Cloud based {{site.data.keyword.lakehouse_short}} instance and include an AWS S3 bucket-based catalog.

The {{site.data.keyword.lakehouse_short}} query engines can run queries on data from AWS S3 buckets. In both cases, you can run the data ingestion and Iceberg-based schema maintenance operations by using AWS EMR Spark.


## About the sample use case
{: #abt_emr_pyfile}

The sample python file (amazon-lakehouse.py) demonstrates creating schema (**amazonschema**), tables, and ingesting data. It also supports table maintenance operations. For more information about the functionalities in the sample, see [About the sample use case](watsonxdata?topic=watsonxdata-run_samp_file#abt_samp_usecase){: external}

## Running the sample use case
{: #abt_emrsamp_run}

Follow the steps to run the Spark sample python file.

1. Connect to the AWS EMR cluster. For more information about using SSH to connect to the EMR cluster, see [Setting up EMR Cluster](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-setting-up.html).

2. Save the following sample python file.

    **Spark sample python file**
    {: #emr_python_file}

    ```python

    from pyspark.sql import SparkSession
    import os

    def init_spark():
    spark = SparkSession.builder.appName("lh-hms-cloud")\
    .enableHiveSupport().getOrCreate()
    return spark

    def create_database(spark):
        # Create a database in the lakehouse catalog
        spark.sql("create database if not exists lakehouse.amazonschema LOCATION 's3a://lakehouse-bucket-amz/'")

    def list_databases(spark):
        # list the database under lakehouse catalog
        spark.sql("show databases from lakehouse").show()

    def basic_iceberg_table_operations(spark):
        # demonstration: Create a basic Iceberg table, insert some data and then query table
        spark.sql("create table if not exists lakehouse.amazonschema.testTable(id INTEGER, name VARCHAR(10), age INTEGER, salary DECIMAL(10, 2)) using iceberg").show()
        spark.sql("insert into lakehouse.amazonschema.testTable values(1,'Alan',23,3400.00),(2,'Ben',30,5500.00),(3,'Chen',35,6500.00)")
        spark.sql("select * from lakehouse.amazonschema.testTable").show()

    def create_table_from_parquet_data(spark):
        # load parquet data into dataframce
        df = spark.read.option("header",True).parquet("s3a://source-bucket-amz/nyc-taxi/yellow_tripdata_2022-01.parquet")
        # write the dataframe into an Iceberg table
        df.writeTo("lakehouse.amazonschema.yellow_taxi_2022").create()
        # describe the table created
        spark.sql('describe table lakehouse.amazonschema.yellow_taxi_2022').show(25)
        # query the table
        spark.sql('select * from lakehouse.amazonschema.yellow_taxi_2022').count()

    def ingest_from_csv_temp_table(spark):
        # load csv data into a dataframe
        csvDF = spark.read.option("header",True).csv("s3a://source-bucket-amz/zipcodes.csv")
        csvDF.createOrReplaceTempView("tempCSVTable")
        # load temporary table into an Iceberg table
        spark.sql('create or replace table lakehouse.amazonschema.zipcodes using iceberg as select * from tempCSVTable')
        # describe the table created
        spark.sql('describe table lakehouse.amazonschema.zipcodes').show(25)
        # query the table
        spark.sql('select * from lakehouse.amazonschema.zipcodes').show()

    def ingest_monthly_data(spark):
        df_feb = spark.read.option("header",True).parquet("s3a://source-bucket-amz//nyc-taxi/yellow_tripdata_2022-02.parquet")
        df_march = spark.read.option("header",True).parquet("s3a://source-bucket-amz//nyc-taxi/yellow_tripdata_2022-03.parquet")
        df_april = spark.read.option("header",True).parquet("s3a://source-bucket-amz//nyc-taxi/yellow_tripdata_2022-04.parquet")
        df_may = spark.read.option("header",True).parquet("s3a://source-bucket-amz//nyc-taxi/yellow_tripdata_2022-05.parquet")
        df_june = spark.read.option("header",True).parquet("s3a://source-bucket-amz//nyc-taxi/yellow_tripdata_2022-06.parquet")

        df_q1_q2 = df_feb.union(df_march).union(df_april).union(df_may).union(df_june)
        df_q1_q2.write.insertInto("lakehouse.amazonschema.yellow_taxi_2022")

    def perform_table_maintenance_operations(spark):
        # Query the metadata files table to list underlying data files
        spark.sql("SELECT file_path, file_size_in_bytes FROM lakehouse.amazonschema.yellow_taxi_2022.files").show()

        # There are many smaller files compact them into files of 200MB each using the
        # `rewrite_data_files` Iceberg Spark procedure
        spark.sql(f"CALL lakehouse.system.rewrite_data_files(table => 'amazonschema.yellow_taxi_2022', options => map('target-file-size-bytes','209715200'))").show()

        # Again, query the metadata files table to list underlying data files; 6 files are compacted
        # to 3 files
        spark.sql("SELECT file_path, file_size_in_bytes FROM lakehouse.amazonschema.yellow_taxi_2022.files").show()

        # List all the snapshots
        # Expire earlier snapshots. Only latest one with comacted data is required
        # Again, List all the snapshots to see only 1 left
        spark.sql("SELECT committed_at, snapshot_id, operation FROM lakehouse.amazonschema.yellow_taxi_2022.snapshots").show()
        #retain only the latest one
        latest_snapshot_committed_at = spark.sql("SELECT committed_at, snapshot_id, operation FROM lakehouse.amazonschema.yellow_taxi_2022.snapshots").tail(1)[0].committed_at
        print (latest_snapshot_committed_at)
        spark.sql(f"CALL lakehouse.system.expire_snapshots(table => 'amazonschema.yellow_taxi_2022',older_than => TIMESTAMP '{latest_snapshot_committed_at}',retain_last => 1)").show()
        spark.sql("SELECT committed_at, snapshot_id, operation FROM lakehouse.amazonschema.yellow_taxi_2022.snapshots").show()

        # Removing Orphan data files
        spark.sql(f"CALL lakehouse.system.remove_orphan_files(table => 'amazonschema.yellow_taxi_2022')").show(truncate=False)

        # Rewriting Manifest Files
        spark.sql(f"CALL lakehouse.system.rewrite_manifests('amazonschema.yellow_taxi_2022')").show()


    def evolve_schema(spark):
        # demonstration: Schema evolution
        # Add column fare_per_mile to the table
        spark.sql('ALTER TABLE lakehouse.amazonschema.yellow_taxi_2022 ADD COLUMN(fare_per_mile double)')
        # describe the table
        spark.sql('describe table lakehouse.amazonschema.yellow_taxi_2022').show(25)


    def clean_database(spark):
        # clean-up the demo database
        spark.sql('drop table if exists lakehouse.amazonschema.testTable purge')
        spark.sql('drop table if exists lakehouse.amazonschema.zipcodes purge')
        spark.sql('drop table if exists lakehouse.amazonschema.yellow_taxi_2022 purge')
        spark.sql('drop database if exists lakehouse.amazonschema cascade')

    def main():
        try:
            spark = init_spark()
            clean_database(spark)

            create_database(spark)
            list_databases(spark)

            basic_iceberg_table_operations(spark)

            # demonstration: Ingest parquet and csv data into a wastonx.data Iceberg table
            create_table_from_parquet_data(spark)
            ingest_from_csv_temp_table(spark)

            # load data for the month of Feburary to June into the table yellow_taxi_2022 created above
            ingest_monthly_data(spark)

            # demonstration: Table maintenance
            perform_table_maintenance_operations(spark)

            # demonstration: Schema evolution
            evolve_schema(spark)
        finally:
            # clean-up the demo database
            #clean_database(spark)
            spark.stop()

    if __name__ == '__main__':
      main()

    ```
    {: codeblock}

1. Run the following commands to download the Hive metastore JAR file from the [location](https://github.com/IBM-Cloud/IBM-Analytics-Engine/tree/master/wxd-connectors/hms-connector) to your workstation:

    The JAR file must be present in the `/home/hadoop` location on all nodes of the cluster. Make a note of the `spark.driver.extraClassPath` and `spark.executor.extraClassPath`.
    {: important}


    ```bash

    wget https://github.com/IBM-Cloud/IBM-Analytics-Engine/raw/master/wxd-connectors/hms-connector/hive-exec-2.3.9-core.jar
    wget https://github.com/IBM-Cloud/IBM-Analytics-Engine/raw/master/wxd-connectors/hms-connector/hive-common-2.3.9.jar
    wget https://github.com/IBM-Cloud/IBM-Analytics-Engine/raw/master/wxd-connectors/hms-connector/hive-metastore-2.3.9.jar
    ```
    {: codeblock}


3. Configure the HMS connection details in the AWS EMR cluster to connect to the {{site.data.keyword.lakehouse_short}} Hive Meta Store (HMS). A sample command to use spark-submit from an EMR-6.12.0 (Spark 3.4.1) based cluster is as follows:

    Run the command from EMR on the EC2 cluster to submit the Sample spark job.

    ```python

    spark-submit \
    --deploy-mode cluster \
    --jars https://repo1.maven.org/maven2/org/apache/iceberg/iceberg-spark-runtime-3.4_2.12/1.4.0/iceberg-spark-runtime-3.4_2.12-1.4.0.jar,/usr/lib/hadoop/hadoop-aws.jar,/usr/share/aws/aws-java-sdk/aws-java-sdk-bundle*.jar,/usr/lib/hadoop-lzo/lib/* \
    --conf spark.sql.catalogImplementation=hive \
    --conf spark.driver.extraClassPath=/home/hadoop/hive-common-2.3.9.jar:/home/hadoop/hive-metastore-2.3.9.jar:/home/hadoop/hive-exec-2.3.9-core.jar \
    --conf spark.executor.extraClassPath=/home/hadoop/hive-common-2.3.9.jar:/home/hadoop/hive-metastore-2.3.9.jar:/home/hadoop/hive-exec-2.3.9-core.jar \
    --conf spark.sql.extensions=org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions \
    --conf spark.sql.iceberg.vectorization.enabled=false \
    --conf spark.sql.catalog.lakehouse=org.apache.iceberg.spark.SparkCatalog \
    --conf spark.sql.catalog.lakehouse.type=hive \
    --conf spark.hive.metastore.uris==<<change_endpoint>> \
    --conf spark.hive.metastore.client.auth.mode=PLAIN \
    --conf spark.hive.metastore.client.plain.username=ibmlhapikey \
    --conf spark.hive.metastore.client.plain.password=<<change_pswd>> \
    --conf spark.hive.metastore.use.SSL=true \
    --conf spark.hive.metastore.truststore.type=JKS \
    --conf spark.hive.metastore.truststore.path=file:///etc/pki/java/cacerts \
    --conf spark.hive.metastore.truststore.password=changeit \
    amazon-lakehouse.py
    ```
    {: codeblock}

Parameter values:

* <<change_endpoint>> : The Hive metastore URI endpoint to access the metastore. For more information on getting the HMS credentials, see [Getting (Hive metastore) HMS Credentials](watsonxdata?topic=watsonxdata-hms){: external}.
* <<change_pswd>> : The password to access the metastore. For more information on getting the HMS credentials, see [Getting (Hive metastore) HMS Credentials](watsonxdata?topic=watsonxdata-hms){: external}.

To run the Spark python file using EMR-6.11.1 (Spark 3.3.2) cluster, download the iceberg jars from the [location](https://repo1.maven.org/maven2/org/apache/iceberg/iceberg-spark-runtime-3.3_2.12/1.4.1/iceberg-spark-runtime-3.3_2.12-1.4.1.jar) and follow the same [procedure](#abt_emrsamp_run).
{: important}
