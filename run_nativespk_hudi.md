---

copyright:
  years: 2017, 2025
lastupdated: "2025-09-19"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Working with different table formats
{: #hudi_nsp}

**Applies to** : [Spark engine]{: tag-blue}  [Gluten accelerated Spark engine]{: tag-green}


The topic describes the procedure to run a Spark application that ingests data into different table formats like Apache Hudi, Apache Iceberg or Delta Lake catalog.

1. Create a storage with the required catalog (catalog can be Apache Hudi, Apache Iceberg or Delta Lake) to store data used in the Spark application. To create storage, see [Adding a storage-catalog pair](/docs/watsonxdata?topic=watsonxdata-reg_bucket).
2. Associate the storage with the Native Spark engine. For more information, see [Associating a catalog with an engine](/docs/watsonxdata?topic=watsonxdata-asso-cat-eng).
3. Create Cloud Object Storage (COS) to store the Spark application. To create Cloud Object Storage and a bucket, see [Creating a storage bucket](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-secure-content-store#create-cos-bucket).
4. Register the Cloud Object Storage in watsonx.data. For more information, see [Adding a storage-catalog pair](/docs/watsonxdata?topic=watsonxdata-reg_bucket).
5. Based on the catalog you select, save the following Spark application (Python file) to your local machine. Here, `iceberg_demo.py`, `hudi_demo.py`, or `delta_demo.py` and upload the Spark application to the COS, see [Uploading data](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-secure-content-store#upload-data).
7. To submit the Spark application with data residing in Cloud Object Storage, specify the parameter values and run the curl command from the following table.



   * **Apache Iceberg**


   The sample file demonstrates the following functionalities:

    * Accessing tables from watsonx.data

    * Ingesting data to watsonx.data

    * Modifying schema in watsonx.data

    Performing table maintenance activities in watsonx.data.

    You must insert the data into the COS bucket. For more information, see [Inserting sample data into the COS bucket](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-upload).

    Python application : [Iceberg Python file](/docs/watsonxdata?topic=watsonxdata-run_samp_file#python_file)



   Curl command to submit Python application :

   **Sample V2 API**

   ```bash
   curl --request POST \
   --url https://<wxd_host_name>/lakehouse/api/v2/spark_engines/<spark_engine_id>/applications \
   --header 'Authorization: Bearer <token>' \
   --header 'Content-Type: application/json' \
   --header 'LhInstanceId: <instance_id>' \
   --data '{  "application_details": {
              "conf": {
                     "spark.hadoop.wxd.apiKey":"Basic <user-authentication-string>"    },
                      "application": "s3a://<application-bucket-name>/iceberg.py"  }
           }'
   ```
   {: codeblock}

   **Sample V3 API**

   ```bash
   curl --request POST \
   --url https://<wxd_host_name>/lakehouse/api/v3/spark_engines/<spark_engine_id>/applications \
   --header 'Authorization: Bearer <token>' \
   --header 'Content-Type: application/json' \
   --header 'LhInstanceId: <instance_id>' \
   --data '{  "application_details": {
              "conf": {
                     "spark.hadoop.wxd.apiKey":"Basic <user-authentication-string>"    },
                      "application": "s3a://<application-bucket-name>/iceberg.py"  }
           }'
   ```
   {: codeblock}

   Parameter values :

   * `<wxd_host_name>`: The hostname of your watsonx.data Cloud instance.

   * `<instance_id>`: The instance ID from the watsonx.data instance URL. For example, 1609968977179454.

   * `<spark_engine_id>`: The Engine ID of the native Spark engine.

   * `<token>`: The bearer token. For more information about generating the token, see [IAM token](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-con-presto-serv#get-ibmiam-token).

   * `<user-authentication-string>`: The value must be base 64 encoded string of user ID and API key . For more information about the format, see the note.



   * **Apache Hudi**

   The Python Spark application demonstrates the following functionality:

   * It creates a database inside the Apache Hudi catalog (that you created to store data). Here, `<database_name>`.

   * It creates a table inside the `<database_name>` database, namely `<table_name>`.

   * It inserts data into the `<table_name>` and does SELECT query operation.

   * It drops the table and schema after use.


   Python application :

   ```bash
   from pyspark.sql import SparkSession
   def init_spark():
       spark = SparkSession.builder.appName("CreateHudiTableInCOS").enableHiveSupport().getOrCreate()
       return spark
   def main():
       try:
           spark = init_spark()
           spark.sql("show databases").show()
           spark.sql("create database if not exists spark_catalog.<database_name> LOCATION 's3a://<data_storage_name>/'").show()
           spark.sql("create table if not exists spark_catalog.<database_name>.<table_name> (id bigint, name string, location string) USING HUDI OPTIONS ('primaryKey' 'id', hoodie.write.markers.type= 'direct', hoodie.embed.timeline.server= 'false')").show()
           spark.sql("insert into <database_name>.<table_name> VALUES (1, 'Sam','Kochi'), (2, 'Tom','Bangalore'), (3, 'Bob','Chennai'), (4, 'Alex','Bangalore')").show()
           spark.sql("select * from spark_catalog.<database_name>.<table_name>").show()
           spark.sql("drop table spark_catalog.<database_name>.<table_name>").show()
           spark.sql("drop schema spark_catalog.<database_name> CASCADE").show()
       finally:
           spark.stop()
   if __name__ == '__main__':
       main()

   ```
   {: codeblock}

   Parameter values:
   * `<database_name>`: Specify the name of the database that you want to create.
   * `<table_name>`: Specify the name of the table that you want to create.
   * `<data_storage_name>`: Specify the name of the Apache Hudi storage that you created.

   Curl command to submit Python application


   **Sample V2 API**

   ``` bash

   curl --request POST
       --url https://<wxd_host_name>/lakehouse/api/v2/spark_engines/<spark_engine_id>/applications
       --header 'Authorization: Bearer <token>'
       --header 'Content-Type: application/json'
       --header 'LhInstanceId: <instance_id>'
       --data '{     "application_details": {
               "conf": {
                       "spark.sql.catalog.spark_catalog.type": "hive",
                       "spark.sql.catalog.spark_catalog": "org.apache.spark.sql.hudi.catalog.HoodieCatalog",
                       "spark.hadoop.wxd.apiKey":"Basic <user-authentication-string>"        },
                       "application": "s3a://<data_storage_name>/hudi_demo.py"    }}
   ```
   {: codeblock}

   **Sample V3 API**

   ``` bash

   curl --request POST
       --url https://<wxd_host_name>/lakehouse/api/v3/spark_engines/<spark_engine_id>/applications
       --header 'Authorization: Bearer <token>'
       --header 'Content-Type: application/json'
       --header 'LhInstanceId: <instance_id>'
       --data '{     "application_details": {
               "conf": {
                       "spark.sql.catalog.spark_catalog.type": "hive",
                       "spark.sql.catalog.spark_catalog": "org.apache.spark.sql.hudi.catalog.HoodieCatalog",
                       "spark.hadoop.wxd.apiKey":"Basic <user-authentication-string>"        },
                       "application": "s3a://<data_storage_name>/hudi_demo.py"    }}
   ```
   {: codeblock}

   Parameter values:

   * `<wxd_host_name>`: The hostname of your watsonx.data Cloud instance.
   * `<instance_id>`: The instance ID from the watsonx.data instance URL. For example, 1609968977179454.
   * `<spark_engine_id>`: The Engine ID of the native Spark engine.
   * `<token>`: The bearer token. For more information about generating the token, see [IAM token](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-con-presto-serv#get-ibmiam-token).
   * `<user-authentication-string>`: The value must be base 64 encoded string of user ID and API key . For more information about the format, see the note.


   * **Delta Lake**

   The Python Spark application demonstrates the following functionality:

   * It creates a database inside the Delta Lake catalog (that you created to store data). Here, `<database_name>`.

   * It creates a table inside the `<database_name>` database, namely `<table_name>`.

   * It inserts data into the `<table_name>` and does SELECT query operation.

   * It drops the table and schema after use.

    Python application :

   ``` bash
   from pyspark.sql import SparkSession
   import os
       def init_spark():
            spark = SparkSession.builder.appName("lh-hms-cloud").enableHiveSupport().getOrCreate()
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

   Parameter values:
   * `<database_name>`: Specify the name of the database that you want to create.
   * `<table_name>`: Specify the name of the table that you want to create.
   * `<data_storage_name>`: Specify the name of the Apache Hudi storage that you created.


   Curl command to submit Python application

   **Sample V2 API**

    ``` bash
   curl --request POST
   --url https://<wxd_host_name>/lakehouse/api/v2/spark_engines/<spark_engine_id>/applications
   --header 'Authorization: Bearer <token>'
   --header 'Content-Type: application/json'
   --header 'LhInstanceId: <instance_id>'
   --data '{        "application_details": {
           "conf": {
           "spark.sql.catalog.spark_catalog" : "org.apache.spark.sql.delta.catalog.DeltaCatalog",
           "spark.sql.catalog.spark_catalog.type" : "hive",
           "spark.hadoop.wxd.apiKey":"<user-authentication-string>"        },
           "application": "s3a://<database_name>/delta_demo.py"        }    }
   ```
   {: codeblock}

   **Sample V3 API**

    ``` bash
   curl --request POST
   --url https://<wxd_host_name>/lakehouse/api/v3/spark_engines/<spark_engine_id>/applications
   --header 'Authorization: Bearer <token>'
   --header 'Content-Type: application/json'
   --header 'LhInstanceId: <instance_id>'
   --data '{        "application_details": {
           "conf": {
           "spark.sql.catalog.spark_catalog" : "org.apache.spark.sql.delta.catalog.DeltaCatalog",
           "spark.sql.catalog.spark_catalog.type" : "hive",
           "spark.hadoop.wxd.apiKey":"<user-authentication-string>"        },
           "application": "s3a://<database_name>/delta_demo.py"        }    }
   ```
   {: codeblock}


   Parameter values

    * `<wxd_host_name>`: The hostname of your watsonx.data Cloud instance.
    * `<instance_id>` : The instance ID from the watsonx.data cluster instance URL. For example, 1609968977179454.
    * `<spark_engine_id>` : The Engine ID of the native Spark engine.
    * `<token>` : The bearer token. For more information about generating the token, see [IAM token](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-con-presto-serv#get-ibmiam-token).
    * `<user-authentication-string>`: The value must be base 64 encoded string of user ID and API key . For more information about the format, see the following note.

   The value of `<user-authentication-string>` must be in the format `echo -n 'ibmlhapikey_<username>:<user_apikey>' | base64`.  Here, `<user_id>` is the IBM Cloud ID of the user whose apikey is used to access the data bucket. The `<IAM_APIKEY>` here is the API key of the user accessing the Object store bucket. To generate API key, log in into the watsonx.data console and navigate to Profile > Profile and Settings > API Keys and generate a new API key. If you generate a new API key, your old API key becomes invalid.
   {: important}

8. After you submit the Spark application, you receive a confirmation message with the application ID and Spark version. Save it for reference.
9. Log in to the watsonx.data cluster, access the Engine details page. In the Applications tab, use application ID to list the application and track the stages. For more information, see [View and manage applications](/docs/watsonxdata?topic=watsonxdata-mng_appltn).


## Related APIs
{: #hudi_nsp_api}

For information on related API, see

* [Create spark engine application](https://cloud.ibm.com/apidocs/watsonxdata-v3#create-spark-engine-application)
