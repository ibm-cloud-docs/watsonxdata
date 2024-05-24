---

copyright:
  years: 2017, 2024
lastupdated: "2024-04-30"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Working with Apache Hudi catalog
{: #hudi_ext_sp}

The topic describes the procedure to run a Spark application that ingests data into an Apache Hudi catalog.

1. Create a storage with Apache Hudi catalog to store data used in the Spark application. To create storage with Apache Hudi catalog, see [Adding a storage-catalog pair](watsonxdata?topic=watsonxdata-reg_bucket).
2. Associate the storage with the external Spark engine. For more information, see [Associating a catalog with an engine](watsonxdata?topic=watsonxdata-asso-cat-eng).
3. Create Cloud Object Storage (COS) to store the Spark application. To create Cloud Object Storage and a bucket, see [Creating a storage bucket](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-secure-content-store#create-cos-bucket).
4. Register the Cloud Object Storage in watsonx.data. For more information, see [Adding a storage-catalog pair](watsonxdata?topic=watsonxdata-reg_bucket).
5. Save the following Spark application (Python file) to your local machine. Here, `hudi_demo.py`.

    The Python Spark application demonstrates the following functionality:
    * It creates a database inside the Apache Hudi catalog (that you created to store data). Here, hudi_db.
    * It creates a table inside the hudi_db database, namely hudi_table.
    * It inserts data into the hudi_table and does SELECT query operation.
    * It drops the table and schema after use.

    ```bash
        from pyspark.sql import SparkSession

        def init_spark():
            spark = SparkSession.builder \
                .appName("CreateHudiTableInCOS") \
                .enableHiveSupport() \
                .getOrCreate()
            return spark

        def main():

            try:
                spark = init_spark()
                spark.sql("show databases").show()
                spark.sql("create database if not exists spark_catalog.hudi_db LOCATION 's3a://hudi-connector-test/'").show()
                spark.sql("create table if not exists spark_catalog.hudi_db.hudi_table (id bigint, name string, location string) USING HUDI OPTIONS ('primaryKey' 'id', hoodie.write.markers.type= 'direct', hoodie.embed.timeline.server= 'false')").show()
                spark.sql("insert into hudi_db.hudi_table VALUES (1, 'Sam','Kochi'), (2, 'Tom','Bangalore'), (3, 'Bob','Chennai'), (4, 'Alex','Bangalore')").show()
                spark.sql("select * from spark_catalog.hudi_db.hudi_table").show()
                spark.sql("drop table spark_catalog.hudi_db.hudi_table").show()
                spark.sql("drop schema spark_catalog.hudi_db CASCADE").show()

            finally:
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
    --data '{
		"conf": {
            "spark.serializer" : "org.apache.spark.serializer.KryoSerializer",
            "spark.hadoop.fs.s3a.bucket.<data_storage_name>.endpoint" : "<your_data_bucket_direct_endpoint>",
            "spark.hadoop.fs.s3a.bucket.<data_storage_name>.access.key" : "<data_bucket_access_key>",
            "spark.hadoop.fs.s3a.bucket.<data_storage_name>.secret.key" : "<data_bucket_secret_key>",
            "spark.hadoop.fs.s3a.path.style.access" : "true",
            "spark.hadoop.fs.s3a.impl" : "org.apache.hadoop.fs.s3a.S3AFileSystem",
            "spark.hive.metastore.uris" : "<metastore URL>",
            "spark.hive.metastore.use.SSL" : "true",
            "spark.hive.metastore.truststore.path" : "file:///opt/ibm/jdk/lib/security/cacerts",
            "spark.hive.metastore.truststore.password" : "changeit",
            "spark.hive.metastore.truststore.type" : "JKS",
            "spark.hive.metastore.client.auth.mode" : "PLAIN",
            "spark.hive.metastore.client.plain.username" : "ibmlhapikey",
            "spark.hive.metastore.client.plain.password" : "<wxd_api_key>",
            "spark.driver.extraJavaOptions" : "-Dcom.sun.jndi.ldap.object.disableEndpointIdentification=true -Djdk.tls.trustNameService=true",
            "spark.executor.extraJavaOptions" : "-Dcom.sun.jndi.ldap.object.disableEndpointIdentification=true -Djdk.tls.trustNameService=true",
            "spark.hadoop.hive.metastore.schema.verification" : "false",
            "spark.hadoop.hive.metastore.schema.verification.record.version" : "false",
        "spark.sql.extensions": "org.apache.spark.sql.hudi.HoodieSparkSessionExtension",
           "spark.kryo.registrator": "org.apache.spark.HoodieSparkKryoRegistrar",
           "spark.sql.catalog.spark_catalog.type": "hudi",
            "spark.sql.catalog.spark_catalog": "org.apache.spark.sql.hudi.catalog.HoodieCatalog"

		},
		"application": "s3a://<data_storage_name>/hudi_demo.py"
	}
    ```
    {: codeblock}

Parameter values:
* `<region>`: The region where you provision the Analytics engine instance.
* `<iae-instance-guid>`: The Analytics engine instance GUID. To get that, see [Retrieving details of a serverless instance](https://test.cloud.ibm.com/docs/AnalyticsEngine?topic=AnalyticsEngine-retrieve-instance-details#retrieve-guid-cli).
* `<token>`: The bearer token. For more information about generating the token, see [IAM token](https://test.cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-con-presto-serv#get-ibmiam-token).
* `<your_data_bucket_direct_endpoint>` : The direct endpoint for accessing the data bucket. Example, s3.us-south.cloud-object-storage.appdomain.cloud for a Cloud Object storage bucket in us-south region. For more information, see [Service credentials](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-service-credentials).
* `<data_bucket_access_key>` : The access key for the Cloud Object storage (data storage). For more information, see [Create HMAC credentials using the CLI](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-uhc-hmac-credentials-main#uhc-create-hmac-credentials-cli).
* `<data_bucket_secret_key>` : The secret key for the Cloud Object storage (data storage). For more information, see [Create HMAC credentials using the CLI](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-uhc-hmac-credentials-main#uhc-create-hmac-credentials-cli).

* `<metastore URL>`: The URL of the catalog.  For more information, see [Getting the HMS endpoint](https://test.cloud.ibm.com/docs-draft/watsonxdata?topic=watsonxdata-hms#hms_url).
* `<wxd_api_key>`: To generate API key, log in into the watsonx.data console and navigate to Profile > Profile and Settings > API Keys and generate a new API key.


8. After you submit the Spark application, you receive a confirmation message with the application ID and Spark version. Save it for reference.
9. Log in to the watsonx.data cluster, access the Engine details page. In the Applications tab, use application ID to list the application and track the stages. For more information, see [View and manage applications](watsonxdata?topic=watsonxdata-mng_appltn).
