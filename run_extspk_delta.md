---

copyright:
  years: 2017, 2025
lastupdated: "2025-12-15"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Working with Delta Lake catalog
{: #delta_ext_sp}


The option to register external Spark engines in watsonx.data is deprecated in this release and will be removed in version 2.3. watsonx.data already includes built-in Spark engines that you can provision and use directly, including the Gluten-accelerated Spark engine and the native watsonx.data Spark engine.
{: important}

The topic describes the procedure to run a Spark application that ingests data into a Delta Lake catalog.

1. Create a storage with Delta Lake catalog to store data used in the Spark application. To create storage with Delta Lake catalog, see [Adding a storage-catalog pair]({{site.data.keyword.ref-reg_bucket-link}}).
2. Associate the storage with the external Spark engine. For more information, see [Associating a catalog with an engine]({{site.data.keyword.ref-asso-cat-eng-link}}).
3. Create Cloud Object Storage (COS) to store the Spark application. To create Cloud Object Storage and a bucket, see [Creating a storage bucket](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-secure-content-store#create-cos-bucket).
4. Register the Cloud Object Storage in watsonx.data. For more information, see [Adding a storage-catalog pair]({{site.data.keyword.ref-reg_bucket-link}}).
5. Save the following Spark application (Python file) to your local machine. Here, `delta_demo.py`.

    The Python Spark application demonstrates the following functionality:
    * It creates a database inside the Delta Lake catalog (that you created to store data). Here, `<database_name>`.
    * It creates a table inside the `<database_name>` database, namely `<table_name>`.
    * It inserts data into the `<table_name>` and does SELECT query operation.
    * It drops the table and schema after use.

   Starting with {{site.data.keyword.lakehouse_short}} version 2.2.0, authentication using `ibmlhapikey` and `ibmlhtoken` as usernames is deprecated. These formats are phased out in 2.3.0 release. To ensure compatibility with upcoming versions, use the new format:`ibmlhapikey_<username>` and `ibmlhtoken_<username>`.
   {: important}

    ```bash
    from pyspark.sql import SparkSession
    import os

    def init_spark():
        spark = SparkSession.builder.appName("lh-hms-cloud")\
        .enableHiveSupport().getOrCreate()

        return spark

    def main():
        spark = init_spark()
        spark.sql("show databases").show()
        spark.sql("create database if not exists spark_catalog.<database_name> LOCATION 's3a://<data_storage_name>/'").show()
        spark.sql("create table if not exists spark_catalog.<database_name>.<table_name> (id bigint, name string, location string) USING DELTA").show()
        spark.sql("insert into spark_catalog.<database_name>.<table_name> VALUES (1, 'Sam','Kochi'), (2, 'Tom','Bangalore'), (3, 'Bob','Chennai'), (4, 'Alex','Bangalore')").show()
        spark.sql("select * from spark_catalog.<database_name>.<table_name>").show()
        spark.sql("drop table spark_catalog.<database_name>.<table_name>").show()
        spark.sql("drop schema spark_catalog.<database_name> CASCADE").show()
        spark.stop()

    if __name__ == '__main__':
        main()
    ```
    {: codeblock}

6. Upload the Spark application to the COS, see [Uploading data](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-secure-content-store#upload-data).
7. To submit the Spark application with data residing in Cloud Object Storage, specify the parameter values and run the following curl command


    ```bash
    curl --request POST \
    --url https://api.<region>.ae.cloud.ibm.com/v3/analytics_engines/<iae-instance-guid>/spark_applications \
    --header 'Authorization: Bearer <token>' \
    --header 'Content-Type: application/json' \
    --header 'LhInstanceId: <instance_id>' \
    --data '{
        "conf": {
                "spark.hadoop.fs.s3a.bucket.<data_storage_name>.access.key" : "<data_bucket_access_key>",
                "spark.hadoop.fs.s3a.bucket.<data_storage_name>.secret.key" : "<data_bucket_secret_key>",
                "spark.hadoop.fs.s3a.bucket.<data_storage_name>.endpoint": "<your_data_bucket_direct_endpoint>",
                "spark.sql.catalogImplementation" : "hive",
                "spark.sql.extensions" : "io.delta.sql.DeltaSparkSessionExtension",
                "spark.serializer" : "org.apache.spark.serializer.KryoSerializer",
                "spark.hadoop.hive.metastore.schema.verification" : "false",
                "spark.hadoop.hive.metastore.schema.verification.record.version" : "false",
                "spark.hadoop.datanucleus.schema.autoCreateTables" : "false",
                "spark.sql.catalog.spark_catalog" : "org.apache.spark.sql.delta.catalog.DeltaCatalog",
                "spark.sql.catalog.spark_catalog.type" : "hive",
                "spark.hive.metastore.uris" : "<metastore URL>",
                "spark.hive.metastore.use.SSL" : "true",
                "spark.hive.metastore.truststore.path" : "file:///opt/ibm/jdk/lib/security/cacerts",
                "spark.hive.metastore.truststore.password" : "changeit",
                "spark.hive.metastore.truststore.type" : "JKS",
                "spark.hive.metastore.client.auth.mode" : "PLAIN",
                "spark.hive.metastore.client.plain.username" : "ibmlhapikey",
                "spark.hive.metastore.client.plain.password" : "<wxd_api_key>",
                "spark.hadoop.fs.s3a.path.style.access" : "true"
        },

        "application": "s3a://<data_storage_name>/delta_demo.py"
        }
    ```
    {: codeblock}

Parameter values:
* `<region>`: The region where you provision the Analytics engine instance.
* `<iae-instance-guid>`: The Analytics engine instance GUID. To get that, see [Retrieving details of a serverless instance](https://cloud.ibm.com/docs/AnalyticsEngine?topic=AnalyticsEngine-retrieve-instance-details#retrieve-guid-cli).
* `<token>`: The bearer token. For more information about generating the token, see [IAM token](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-con-presto-serv#get-ibmiam-token).
* `<your_data_bucket_direct_endpoint>` : The direct endpoint for accessing the data bucket. Example, s3.us-south.cloud-object-storage.appdomain.cloud for a Cloud Object storage bucket in us-south region. For more information, see [Service credentials](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-service-credentials).
* `<data_bucket_access_key>` : The access key for the Cloud Object storage (data storage). For more information, see [Create HMAC credentials using the CLI](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-uhc-hmac-credentials-main#uhc-create-hmac-credentials-cli).
* `<data_bucket_secret_key>` : The secret key for the Cloud Object storage (data storage). For more information, see [Create HMAC credentials using the CLI](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-uhc-hmac-credentials-main#uhc-create-hmac-credentials-cli).

* `<metastore URL>`: The URL of the catalog.  For more information, see [Getting the MDS endpoint]({{site.data.keyword.ref-hms-link}}).
* `<wxd_api_key>`: To generate API key, log in into the watsonx.data console and navigate to Profile > Profile and Settings > API Keys and generate a new API key.



8. After you submit the Spark application, you receive a confirmation message with the application ID and Spark version. Save it for reference.
9. Log in to the watsonx.data cluster, access the Engine details page. In the Applications tab, use application ID to list the application and track the stages. For more information, see [View and manage applications]({{site.data.keyword.ref-mng_appltn-link}}).
