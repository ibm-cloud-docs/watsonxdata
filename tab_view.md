---

copyright:
  years: 2017, 2024
lastupdated: "2024-05-31"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Tab view
{: #view}

## Working with Apache Hudi catalog
{: #hudi_nsp}
{: hudi}



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
    --url https://<wxd_host_name>/lakehouse/api/v2/spark_engines/<spark_engine_id>/applications \
    --header 'Authorization: Bearer <token>' \
    --header 'Content-Type: application/json' \
    --header 'LhInstanceId: <instance_id>' \
    --data '{
        "application_details": {
            "conf": {
            "spark.serializer" : "org.apache.spark.serializer.KryoSerializer",
            "spark.hadoop.fs.s3a.path.style.access" : "true",
            "spark.hive.metastore.client.plain.username":"ibmlhapikey",
            "spark.hive.metastore.client.plain.password":"<wxd_api_key>",
            "spark.driver.extraJavaOptions" : "-Dcom.sun.jndi.ldap.object.disableEndpointIdentification=true -Djdk.tls.trustNameService=true",
            "spark.executor.extraJavaOptions" : "-Dcom.sun.jndi.ldap.object.disableEndpointIdentification=true -Djdk.tls.trustNameService=true",

            "spark.kryo.registrator": "org.apache.spark.HoodieSparkKryoRegistrar",
            "spark.sql.catalog.spark_catalog.type": "hudi",
            "spark.sql.catalog.spark_catalog": "org.apache.spark.sql.hudi.catalog.HoodieCatalog",

            "spark.hadoop.wxd.cas.endpoint":"<cas_endpoint>/cas/v1/signature",
            "spark.hadoop.wxd.cas.apiKey":"<user-authentication-string>"

            },
            "application": "s3a://hudi-connector-test/hudi_demo.py"
        }
    }
    ```
    {: codeblock}

Parameter values:
* `<wxd_host_name>`: The hostname of your watsonx.data Cloud instance.
* `<instance_id>`: The instance ID from the watsonx.data instance URL. For example, 1609968977179454.
* `<spark_engine_id>`: The Engine ID of the native Spark engine.
* `<token>`: The bearer token. For more information about generating the token, see [IAM token](https://test.cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-con-presto-serv#get-ibmiam-token).
* `<wxd_api_key>`: To generate API key, log in into the watsonx.data console and navigate to Profile > Profile and Settings > API Keys and generate a new API key.
* `<cas_endpoint>`: The CAS endpoint. To generate CAS endpoint, see [Content Aware Storage (CAS) endpoint](watsonxdata?topic=watsonxdata-cas_ep).
* `<user-authentication-string>`: The value must be in the format : `base64 encoding(ibmlhapikey_<wxd-user-name>:<user_apikey>)`. To generate API key, log in into the watsonx.data console and navigate to Profile > Profile and Settings > API Keys and generate a new API key.
 If you generate a new API key, your old API key becomes invalid. If you generate the encoded string from a Mac machine, remove last 4 characters from resulted string.
 {: note}


8. After you submit the Spark application, you receive a confirmation message with the application ID and Spark version. Save it for reference.
9. Log in to the watsonx.data cluster, access the Engine details page. In the Applications tab, use application ID to list the application and track the stages. For more information, see [View and manage applications](watsonxdata?topic=watsonxdata-mng_appltn).

## Working with Apache Delta catalog
{: #delta}
{: deltalake}



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
    --url https://<wxd_host_name>/lakehouse/api/v2/spark_engines/<spark_engine_id>/applications \
    --header 'Authorization: Bearer <token>' \
    --header 'Content-Type: application/json' \
    --header 'LhInstanceId: <instance_id>' \
    --data '{
        "application_details": {
            "conf": {
            "spark.serializer" : "org.apache.spark.serializer.KryoSerializer",
            "spark.hadoop.fs.s3a.path.style.access" : "true",
            "spark.hive.metastore.client.plain.username":"ibmlhapikey",
            "spark.hive.metastore.client.plain.password":"<wxd_api_key>",
            "spark.driver.extraJavaOptions" : "-Dcom.sun.jndi.ldap.object.disableEndpointIdentification=true -Djdk.tls.trustNameService=true",
            "spark.executor.extraJavaOptions" : "-Dcom.sun.jndi.ldap.object.disableEndpointIdentification=true -Djdk.tls.trustNameService=true",

            "spark.kryo.registrator": "org.apache.spark.HoodieSparkKryoRegistrar",
            "spark.sql.catalog.spark_catalog.type": "hudi",
            "spark.sql.catalog.spark_catalog": "org.apache.spark.sql.hudi.catalog.HoodieCatalog",

            "spark.hadoop.wxd.cas.endpoint":"<cas_endpoint>/cas/v1/signature",
            "spark.hadoop.wxd.cas.apiKey":"<user-authentication-string>"

            },
            "application": "s3a://hudi-connector-test/hudi_demo.py"
        }
    }
    ```
    {: codeblock}

Parameter values:
* `<wxd_host_name>`: The hostname of your watsonx.data Cloud instance.
* `<instance_id>`: The instance ID from the watsonx.data instance URL. For example, 1609968977179454.
* `<spark_engine_id>`: The Engine ID of the native Spark engine.
* `<token>`: The bearer token. For more information about generating the token, see [IAM token](https://test.cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-con-presto-serv#get-ibmiam-token).
* `<wxd_api_key>`: To generate API key, log in into the watsonx.data console and navigate to Profile > Profile and Settings > API Keys and generate a new API key.
* `<cas_endpoint>`: The CAS endpoint. To generate CAS endpoint, see [Content Aware Storage (CAS) endpoint](watsonxdata?topic=watsonxdata-cas_ep).
* `<user-authentication-string>`: The value must be in the format : `base64 encoding(ibmlhapikey_<wxd-user-name>:<user_apikey>)`. To generate API key, log in into the watsonx.data console and navigate to Profile > Profile and Settings > API Keys and generate a new API key.
 If you generate a new API key, your old API key becomes invalid. If you generate the encoded string from a Mac machine, remove last 4 characters from resulted string.
 {: note}


8. After you submit the Spark application, you receive a confirmation message with the application ID and Spark version. Save it for reference.
9. Log in to the watsonx.data cluster, access the Engine details page. In the Applications tab, use application ID to list the application and track the stages. For more information, see [View and manage applications](watsonxdata?topic=watsonxdata-mng_appltn).


## Working with Iceberg catalog
{: #iceberg}
{: iceberg}



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
    --url https://<wxd_host_name>/lakehouse/api/v2/spark_engines/<spark_engine_id>/applications \
    --header 'Authorization: Bearer <token>' \
    --header 'Content-Type: application/json' \
    --header 'LhInstanceId: <instance_id>' \
    --data '{
        "application_details": {
            "conf": {
            "spark.serializer" : "org.apache.spark.serializer.KryoSerializer",
            "spark.hadoop.fs.s3a.path.style.access" : "true",
            "spark.hive.metastore.client.plain.username":"ibmlhapikey",
            "spark.hive.metastore.client.plain.password":"<wxd_api_key>",
            "spark.driver.extraJavaOptions" : "-Dcom.sun.jndi.ldap.object.disableEndpointIdentification=true -Djdk.tls.trustNameService=true",
            "spark.executor.extraJavaOptions" : "-Dcom.sun.jndi.ldap.object.disableEndpointIdentification=true -Djdk.tls.trustNameService=true",

            "spark.kryo.registrator": "org.apache.spark.HoodieSparkKryoRegistrar",
            "spark.sql.catalog.spark_catalog.type": "hudi",
            "spark.sql.catalog.spark_catalog": "org.apache.spark.sql.hudi.catalog.HoodieCatalog",

            "spark.hadoop.wxd.cas.endpoint":"<cas_endpoint>/cas/v1/signature",
            "spark.hadoop.wxd.cas.apiKey":"<user-authentication-string>"

            },
            "application": "s3a://hudi-connector-test/hudi_demo.py"
        }
    }
    ```
    {: codeblock}

Parameter values:
* `<wxd_host_name>`: The hostname of your watsonx.data Cloud instance.
* `<instance_id>`: The instance ID from the watsonx.data instance URL. For example, 1609968977179454.
* `<spark_engine_id>`: The Engine ID of the native Spark engine.
* `<token>`: The bearer token. For more information about generating the token, see [IAM token](https://test.cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-con-presto-serv#get-ibmiam-token).
* `<wxd_api_key>`: To generate API key, log in into the watsonx.data console and navigate to Profile > Profile and Settings > API Keys and generate a new API key.
* `<cas_endpoint>`: The CAS endpoint. To generate CAS endpoint, see [Content Aware Storage (CAS) endpoint](watsonxdata?topic=watsonxdata-cas_ep).
* `<user-authentication-string>`: The value must be in the format : `base64 encoding(ibmlhapikey_<wxd-user-name>:<user_apikey>)`. To generate API key, log in into the watsonx.data console and navigate to Profile > Profile and Settings > API Keys and generate a new API key.
 If you generate a new API key, your old API key becomes invalid. If you generate the encoded string from a Mac machine, remove last 4 characters from resulted string.
 {: note}


8. After you submit the Spark application, you receive a confirmation message with the application ID and Spark version. Save it for reference.
9. Log in to the watsonx.data cluster, access the Engine details page. In the Applications tab, use application ID to list the application and track the stages. For more information, see [View and manage applications](watsonxdata?topic=watsonxdata-mng_appltn).
