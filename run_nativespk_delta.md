---

copyright:
  years: 2017, 2024
lastupdated: "2024-05-31"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Working with Delta Lake catalog
{: #delta_nsp}

The topic describes the procedure to run a Spark application that ingests data into a Delta Lake catalog.

1. Create a storage with Delta Lake catalog to store data used in the Spark application. To create storage with Delta Lake catalog, see [Adding a storage-catalog pair](watsonxdata?topic=watsonxdata-reg_bucket).
2. Associate the storage with the Native Spark engine. For more information, see [Associating a catalog with an engine](watsonxdata?topic=watsonxdata-asso-cat-eng).
3. Create Cloud Object Storage (COS) to store the Spark application. To create Cloud Object Storage and a bucket, see [Creating a storage bucket](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-secure-content-store#create-cos-bucket).
4. Register the Cloud Object Storage in watsonx.data. For more information, see [Adding a storage-catalog pair](watsonxdata?topic=watsonxdata-reg_bucket).
5. Save the following Spark application (Python file) to your local machine. Here, `delta_demo.py`.

    The Python Spark application demonstrates the following functionality:
    * It creates a database inside the Delta Lake catalog (that you created to store data). Here, `iae`.
    * It creates a table inside the `iae` database, namely `employee`.
    * It inserts data into the `employee` and does SELECT query operation.
    * It drops the table and schema after use.

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
        spark.sql("create database if not exists spark_catalog.iae LOCATION 's3a://delta-connector-test/'").show()
        spark.sql("create table if not exists spark_catalog.iae.employee (id bigint, name string, location string) USING DELTA").show()
        spark.sql("insert into spark_catalog.iae.employee VALUES (1, 'Sam','Kochi'), (2, 'Tom','Bangalore'), (3, 'Bob','Chennai'), (4, 'Alex','Bangalore')").show()
        spark.sql("select * from spark_catalog.iae.employee").show()
        spark.sql("drop table spark_catalog.iae.employee").show()
        spark.sql("drop schema spark_catalog.iae CASCADE").show()
        spark.stop()

    if __name__ == '__main__':
        main()
    ```
    {: codeblock}

6. Upload the Spark application to the COS, see [Uploading data](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-secure-content-store#upload-data).
7. To submit the Spark application with data residing in Cloud Object Storage, specify the parameter values and run the following curl command


    ```bash
    curl --request POST \
    --url https://<wxd_host_name>/lakehouse/api/v2/spark_engines/<spark_engine_id>/applications \
    --header 'Authorization: Bearer <token>' \
    --header 'Content-Type: application/json' \
    --header 'LhInstanceId: <instance_id>' \
    --data '{
        "application_details": {
        "conf": {
                "spark.sql.catalog.spark_catalog" : "org.apache.spark.sql.delta.catalog.DeltaCatalog",
                "spark.sql.catalog.spark_catalog.type" : "hive",
                "spark.hive.metastore.client.plain.username" : "ibmlhapikey",
                "spark.hive.metastore.client.plain.password" : "<wxd_api_key>",
                "spark.hadoop.wxd.cas.endpoint":"<cas_endpoint>/cas/v1/signature",
                "spark.hadoop.wxd.cas.apiKey":"base64 encoding(ibmlhapikey_<username>:<user_apikey>)"
        },

        "application": "s3a://delta-connector-test/delta_demo.py"
        }
    }
    ```
    {: codeblock}

Parameter values:
* `<wxd_host_name>`: The hostname of your watsonx.data Cloud instance.
* `<instance_id>` : The instance ID from the watsonx.data cluster instance URL. For example, 1609968977179454.
* `<spark_engine_id>` : The Engine ID of the native Spark engine.
* `<token>` : The bearer token. For more information about generating the token, see [IAM token](https://test.cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-con-presto-serv#get-ibmiam-token).
* `<wxd_api_key>`: To generate API key, log in into the watsonx.data console and navigate to Profile > Profile and Settings > API Keys and generate a new API key.
* `<cas_endpoint>`: The CAS endpoint. To generate CAS endpoint, see [Content Aware Storage (CAS) endpoint](watsonxdata?topic=watsonxdata-cas_ep).
* `<user-authentication-string>`: The value must be in the format : `base64 encoding(ibmlhapikey_<wxd-user-name>:<user_apikey>)`. To generate API key, log in into the watsonx.data console and navigate to Profile > Profile and Settings > API Keys and generate a new API key.
 If you generate a new API key, your old API key becomes invalid. If you generate the encoded string from a Mac machine, remove last 4 characters from resulted string.
 {: note}

8. After you submit the Spark application, you receive a confirmation message with the application ID and Spark version. Save it for reference.
9. Log in to the watsonx.data cluster, access the Engine details page. In the Applications tab, use application ID to list the application and track the stages. For more information, see [View and manage applications](watsonxdata?topic=watsonxdata-mng_appltn).
