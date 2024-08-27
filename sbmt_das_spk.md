---

copyright:
  years: 2017, 2024
lastupdated: "2024-08-27"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Submitting Spark application by using native Spark engine
{: #smbit_nsp_1}

This topic provides the procedure to submit a Spark application by using native Spark engine.

## Prerequisites
{: #nsppk_preq_1}

* Metastore admin role : To enable your Spark application to work with the watsonx.data catalog and storage, you must have `Metastore admin` role. Without `Metastore admin` privilege, you cannot ingest data to storage by using Native Spark engine. For more information about the Spark configuration, see [Working with the watsonx.data catalog and storage](#view_smbit_nsp).

* Create an object storage : To store the Spark application and related output, create a storage bucket. To create Cloud Object Storage and a bucket, see [Creating a storage bucket](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-secure-content-store#create-cos-bucket). Maintain separate storage for application and data. Register only data buckets with {{site.data.keyword.lakehouse_short}}.

* Register the Cloud Object Storage : Register Cloud Object Storage bucket in {{site.data.keyword.lakehouse_short}}. To register Cloud Object Storage bucket, see [Adding bucket catalog pair](watsonxdata?topic=watsonxdata-reg_bucket).

    You can create different Cloud Object Storage buckets to store application code and the output. Register the data bucket, which stores the input data, and watsonx.data tables. You need not register the storage bucket, which maintains the application code with watsonx.data.
    {: note}


### Submitting a Spark application without accessing the watsonx.data catalog
{: #nsppk_preq_3}

You can submit a Spark application by running a CURL command. Complete the following steps to submit a Python application.

Run the following curl command to submit the word count application.



    ```bash
    curl --request POST --url
    https://<region>.lakehouse.cloud.ibm.com/lakehouse/api/v2/spark_engines/<spark_engine_id>/a
    pplications --header 'Authorization: Bearer <token>' --header 'Content-Type: application/json'
    --header 'AuthInstanceID: <crn_instance>' --data '{
    "application_details": {
    "application": "/opt/ibm/spark/examples/src/main/python/wordcount.py",
    "arguments": [
    "/opt/ibm/spark/examples/src/main/resources/people.txt"
    ]
    }
    }'
    ```
    {: codeblock}

    Parameters:

    * `<crn_instance>` : The CRN of the watsonx.data instance.
    * `<region>`: The region where the Spark instance is provisioned.
    * `<spark_engine_id>` : The engine ID of the Spark engine.
    * `<token>` : The bearer token. For more information about generating the token, see Generating a bearer token.

### Submitting a Spark application by accessing the watsonx.data catalog
{: #nsppk_preq_2}

To access data from a catalog that is associated with the Spark engine and perform some basic operations on that catalog, do the following:

Run the following curl command:


```bash
    curl --request POST --url
    https://<region>.lakehouse.cloud.ibm.com/lakehouse/api/v2/spark_engines/<spark_engine_id>/a
    pplications --header 'Authorization: Bearer <token>' --header 'Content-Type: application/json'
    --header 'AuthInstanceID: <crn_instance>' --data '{
    "application_details": {
    "conf": {
    "spark.hadoop.wxd.apiKey":"Basic <encoded-api-key>"
    },
    "application": "s3a://<application-bucket-name>/iceberg.py"
    }
    }
```
{: codeblock}



   Parameter values:
   * `<encoded-api-key>` : The value must be in the format `echo -n"ibmlhapikey_<user_id>:<user’s api key>" | base64`. Here, <user_id> is the IBM Cloud ID of the user whose api key is used to access the data bucket. The `<IAM_APIKEY>` here is the API key of the user accessing the Object store bucket. To generate an API key, login into the watsonx.data console and navigate to Profile > Profile and Settings > API Keys and generate a new API key.
   * `<application_bucket_name>` : The name of the object storage containing your application code. You must pass the credentials of this storage if it is not registered with watsonx.data.


### Sample Python application for Iceberg catalog Operations
{: #nsppk_preq_5}

The following is the sample Python application to perform basic operations on data stored in an Iceberg catalog:


```bash
    from pyspark.sql import SparkSession
    import os
    from datetime import datetime
    def init_spark():
    spark = SparkSession.builder.appName("lh-hms-cloud").enableHiveSupport().getOrCreate()
    return spark
    def create_database(spark,bucket_name,catalog):
    spark.sql(f"create database if not exists {catalog}.<db_name> LOCATION 's3a://{bucket_name}/'")
    def list_databases(spark,catalog):
    spark.sql(f"show databases from {catalog}").show()
    def basic_iceberg_table_operations(spark,catalog):
    spark.sql(f"create table if not exists {catalog}.<db_name>.<table_name>(id INTEGER, name
    VARCHAR(10), age INTEGER, salary DECIMAL(10, 2)) using iceberg").show()
    spark.sql(f"insert into {catalog}.<db_name>.<table_name>
    values(1,'Alan',23,3400.00),(2,'Ben',30,5500.00),(3,'Chen',35,6500.00)")
    spark.sql(f"select * from {catalog}.<db_name>.<table_name>").show()
    def clean_database(spark,catalog):
    spark.sql(f'drop table if exists {catalog}.<db_name>.<table_name> purge')
    spark.sql(f'drop database if exists {catalog}.<db_name> cascade')
    def main():
    try:
    spark = init_spark()
    create_database(spark,"<wxd-data-bucket-name>","<wxd-data-bucket-catalog-name>")
    list_databases(spark,"<wxd-data-bucket-catalog-name>")
    basic_iceberg_table_operations(spark,"<wxd-data-bucket-catalog-name>")
    finally:
    clean_database(spark,"<wxd-data-bucket-catalog-name>")
    spark.stop()
    if __name__ == '__main__':
    main()
```
{: codeblock}


## Accessing a non-catalog based storage
{: #view_smbit_nsp-2}

To access watsonx.data storage without using DAS, or to access the data from a non-catalog storage, pass HMAC credentials (access and secret keys) of the data bucket.

```bash
curl --request POST --url
https://<region>.lakehouse.cloud.ibm.com/lakehouse/api/v2/spark_engines/<spark_engine_id>/a
pplications --header 'Authorization: Bearer <token>' --header 'Content-Type: application/json'
--header 'AuthInstanceID: <crn_instance>' --data '{
"application_details": {
"application": "s3a://<application-bucket-name>/cos-read.py",
"conf": {
"spark.hadoop.fs.s3a.bucket.<data-bucket-name>.endpoint": "<cos_endpoint>",
"spark.hadoop.fs.s3a.bucket.<data-bucket-name>.access.key": "<s3 bucket HMAC access
key>",
"spark.hadoop.fs.s3a.bucket.<data-bucket-name>.secret.key": "<s3 bucket HMAC secret
key>",
"spark.app.name": "reader-app"
}
}
}'
```
{: codeblock}

Parameters:
* `<cos_endpoint>`: The endpoint URL for your Cloud Object Storage.
* `<s3-bucket-HMAC-access-key>`: HMAC access key for the S3 bucket.
* `<s3-bucket-HMAC-secret-key>`: HMAC secret key for the S3 bucket.
