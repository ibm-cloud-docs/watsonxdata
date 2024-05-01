---

copyright:
  years: 2017, 2024
lastupdated: "2024-04-30"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Submitting Spark application by using CAS to access data
{: #smbit_cas_nsp}

You can submit Spark application by accessing watsonx.data data without object store credentials. If the Spark application (that you want to submit) uses data that resides in an Object Store (COS, AWS S3 and Minio), you can use Content Aware Storage (CAS) to access the data (without using the object store credentials) and submit the application.

## Prerequisites
{: #smbit_cas_preq}

1. Create Cloud Object Storage to store data used in the Spark application. To create Cloud Object Storage and a bucket, see [Creating a storage bucket](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-secure-content-store#create-cos-bucket). You can provision two buckets, data-bucket to store watsonx.data tables and application bucket to maintain Spark application code.
2. Register Cloud Object Storage bucket (that stores data) in watsonx.data. For more information, see [Adding bucket catalog pair](watsonxdata?topic=watsonxdata-reg_bucket).
3. Upload the Spark application to the Cloud Object Storage application bucket, see [Uploading data](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-secure-content-store#upload-data).

## Submit Spark application
{: #smbit_cas_nsp_1}

1. To submit the Spark application with data residing in Cloud Object Storage (without accessing object store credentials), specify the parameter values and run the following curl command. The following example shows the command to submit `iceberg.py` application.


    Example 1:

    ```bash
    curl --request POST \
      --url https://<region>.lakehouse.cloud.ibm.com/lakehouse/api/v2/spark_engines/<spark_engine_id>/applications \
      --header 'Authorization: Bearer <token>' \
      --header 'Content-Type: application/json' \
      --header 'AuthInstanceID: <crn_instance>' \
      --data '{
      "application_details": {
      "conf": {
            "spark.hadoop.fs.s3a.bucket.<wxd-data-bucket-name>.endpoint": "<wxd-data-bucket-endpoint>",
            "spark.hadoop.fs.s3a.bucket.<user-application-bucket-name>.endpoint": "<user-application-bucket-endpoint>",
            "spark.hadoop.fs.s3a.bucket.<user-application-bucket-name>.access.key": "<user-application-bucket-accesskey>",
            "spark.hadoop.fs.s3a.bucket.<user-application-bucket-name>.secret.key": "<user-application-bucket-secretkey>",
            "spark.sql.catalogImplementation": "hive",
          "spark.sql.extensions":"org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions",
          "spark.sql.iceberg.vectorization.enabled":"false",
            "spark.sql.catalog.<wxd-bucket-catalog-name>":"org.apache.iceberg.spark.SparkCatalog",
          "spark.sql.catalog.<wxd-bucket-catalog-name>.type":"hive",
          "spark.sql.catalog.<wxd-bucket-catalog-name>.uri":"thrift://ibm-lh-lakehouse-hive-metastore-svc.cpd-instance.svc.cluster.local:9083",
          "spark.hive.metastore.client.auth.mode":"PLAIN",
          "spark.hive.metastore.client.plain.username":"cpadmin",
          "spark.hive.metastore.client.plain.password":"xxx",
          "spark.hive.metastore.use.SSL":"true",
          "spark.hive.metastore.truststore.type":"JKS",
          "spark.hive.metastore.truststore.path":"file:///opt/ibm/jdk/lib/security/cacerts",
          "spark.hive.metastore.truststore.password":"changeit",
            "spark.hadoop.fs.s3a.bucket.<wxd-data-bucket-name>.aws.credentials.provider":"com.ibm.iae.s3.credentialprovider.WatsonxCredentialsProvider",
            "spark.hadoop.fs.s3a.bucket.<wxd-data-bucket-name>.custom.signers":"WatsonxAWSV4Signer:com.ibm.iae.s3.credentialprovider.WatsonxAWSV4Signer",
            "spark.hadoop.fs.s3a.bucket.<wxd-data-bucket-name>.s3.signing-algorithm":"WatsonxAWSV4Signer",
            "spark.hadoop.wxd.cas.endpoint":"<cas_endpoint>/cas/v1/signature",
            "spark.hadoop.wxd.instanceId":"1711014406109108",
            "spark.hadoop.wxd.cas.apiKey":"xxx"
        },
        "application": "s3a://<user-application-bucket-name>/iceberg.py"
      }
    }
    ```
    {: codeblock}

    Parameters:
    * `<region>`: The region where the Spark instance is provisioned.
    * `<spark_engine_id>` : The Engine ID of the native Spark engine.
    * `<token>` : The bearer token. For more information about generating the token, see [Generating a bearer token](https://cloud.ibm.com/apidocs/watsonxdata#authentication).
    * `<crn_instance>` : The CRN of the watsonx.data instance.
    * `<cos_endpoint>`: The direct endpoint of the Cloud Object Storage bucket. For example, s3.direct.us-south.cloud-object-storage.appdomain.cloud.
    * `<cas_endpoint>` : The Content Aware Storage (CAS) endpoint. To get the CAS endpoint, see [Getting CAS endpoint](watsonxdata?topic=watsonxdata-cas_ep).
    * `<username>` : The username for your watsonx.data instance. Here, ibmlhapikey.
    * `<apikey>` : The base64 encoded `ibmlhapikey_<user_id>:<IAM_APIKEY>. Here, <user_id> is the IBM Cloud id of the user whose apikey is used to access the data bucket. To generate <IAM_APIKEY>, see [Getting CAS endpoint](watsonxdata?topic=watsonxdata-cas_ep).
    * `<user-application-bucket-name>` : The name of the Cloud Object Storage.
    * `<python file name>` : The Spark application file name.


    **Python application**

    The following is the sample Python application, iceberg.py that fetch data from watsonx.data bucket and perform some operations.

    ```bash
    from pyspark.sql import SparkSession
    import os
    from datetime import datetime

    def init_spark():
        spark = SparkSession.builder.appName("lh-hms-cloud").enableHiveSupport().getOrCreate()
        return spark

    def create_database(spark,bucket_name,catalog):
        spark.sql(f"create database if not exists {catalog}.ivttestdb LOCATION 's3a://{bucket_name}/'")

    def list_databases(spark,catalog):
        # list the database under lakehouse catalog
        spark.sql(f"show databases from {catalog}").show()

    def basic_iceberg_table_operations(spark,catalog):
        # demonstration: Create a basic Iceberg table, insert some data and then query table
        print("creating table")
        spark.sql(f"create table if not exists {catalog}.ivttestdb.testTable(id INTEGER, name VARCHAR(10), age INTEGER, salary DECIMAL(10, 2)) using iceberg").show()
        print("table created")
        spark.sql(f"insert into {catalog}.ivttestdb.testTable values(1,'Alan',23,3400.00),(2,'Ben',30,5500.00),(3,'Chen',35,6500.00)")
        print("data inserted")
        spark.sql(f"select * from {catalog}.ivttestdb.testTable").show()



    def clean_database(spark,catalog):
        # clean-up the demo database
        spark.sql(f'drop table if exists {catalog}.ivttestdb.testTable purge')
        spark.sql(f'drop database if exists {catalog}.ivttestdb cascade')

    def main():
        try:
            spark = init_spark()

            create_database(spark,"<wxd-data-bucket-name>","<wxd-data-bucket-catalog-name>")
            list_databases(spark,"<wxd-data-bucket-catalog-name>")
            basic_iceberg_table_operations(spark,"<wxd-data-bucket-catalog-name>")


        finally:
            # clean-up the demo database
            clean_database(spark,"<wxd-data-bucket-catalog-name>")
            spark.stop()

    if __name__ == '__main__':
        main()
        ```
        {: codeblock}

5. After you submit the Spark application, you receive a confirmation message with the application ID and Spark version. Save it for reference.
6. Log in to the watsonx.data cluster, access the Engine details page. In the Applications tab, use the application ID to list the application and you can track the stages. For more information, see [View and manage applications](watsonxdata?topic=watsonxdata-mng_appltn).


## Working with the watsonx.data catalog and storage
{: #view_smbit_nsp}

To enable your Spark application to work with the watsonx.data catalog and storage, add the following configuration to your application payload:

```bash
spark.hive.metastore.client.plain.username=ibmlhapikey
spark.hive.metastore.client.plain.password=<api-key-of-the-user-which-has-metastore-admin-role>
spark.hadoop.wxd.apiKey=Basic base64(ibmlhapikey_ibmcloudid:apikey)
```
{: codeblock}
