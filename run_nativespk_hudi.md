---

copyright:
  years: 2017, 2024
lastupdated: "2024-10-23"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Working with different table formats
{: #hudi_nsp}

The topic describes the procedure to run a Spark application that ingests data into different table formats like Apache Hudi, Apache Iceberg or Delta Lake catalog.

1. Create a storage with the required catalog (catalog can be Apache Hudi, Apache Iceberg or Delta Lake) to store data used in the Spark application. To create storage, see [Adding a storage-catalog pair](watsonxdata?topic=watsonxdata-reg_bucket).
2. Associate the storage with the Native Spark engine. For more information, see [Associating a catalog with an engine](watsonxdata?topic=watsonxdata-asso-cat-eng).
3. Create Cloud Object Storage (COS) to store the Spark application. To create Cloud Object Storage and a bucket, see [Creating a storage bucket](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-secure-content-store#create-cos-bucket).
4. Register the Cloud Object Storage in watsonx.data. For more information, see [Adding a storage-catalog pair](watsonxdata?topic=watsonxdata-reg_bucket).
5. Based on the catalog you select, save the following Spark application (Python file) to your local machine. Here, `iceberg_demo.py`, `hudi_demo.py`, or `delta_demo.py` and upload the Spark application to the COS, see [Uploading data](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-secure-content-store#upload-data).
7. To submit the Spark application with data residing in Cloud Object Storage, specify the parameter values and run the curl command from the following table.

|Apache Iceberg| |
|-----|-----|
| `iceberg_demo.py` | The sample file demonstrates the following functionalities: \n * Accessing tables from watsonx.data \n * Ingesting data to watsonx.data \n * Modifying schema in watsonx.data \n Performing table maintenance activities in watsonx.data. \n You must insert the data into the COS bucket. For more information, see [Inserting sample data into the COS bucket](watsonxdata?topic==watsonxdata-run_samp_file#insert_samp_usecase). \n  \n Python application : [Iceberg Python file](watsonxdata?topic=watsonxdata-run_samp_file#python_file) |
| Curl command to submit Python application | ```\n \n \n \n    curl --request POST     --url https://<wxd_host_name>/lakehouse/api/v2/spark_engines/<spark_engine_id>/applications \n \n     --header 'Authorization: Bearer <token>' \n \n    --header 'Content-Type: application/json' \n \n    --header 'LhInstanceId: <instance_id>' \n \n    --data '{  "application_details": {\n \n    "conf": {\n \n        "spark.hive.metastore.client.plain.username":"cpadmin",\n \n        "spark.hive.metastore.client.plain.password":"xxx",\n \n        "spark.hadoop.wxd.cas.apiKey":"ZenApikey xxx"    },\n \n    "application": "s3a://shivangi-cas-iceberg-test/iceberg.py"  }} \n``` |
| Parameter values | Parameter values: \n * `<wxd_host_name>`: The hostname of your watsonx.data Cloud instance. \n * `<instance_id>`: The instance ID from the watsonx.data instance URL. For example, 1609968977179454. \n * `<spark_engine_id>`: The Engine ID of the native Spark engine. \n * `<token>`: The bearer token. For more information about generating the token, see [IAM token](https://test.cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-con-presto-serv#get-ibmiam-token). \n * `<wxd_api_key>`: To generate API key, log in into the watsonx.data console and navigate to Profile > Profile and Settings > API Keys and generate a new API key. \n * `<cas_endpoint>`: The DAS endpoint. To generate DAS endpoint, see [Data Access Service (DAS) endpoint](watsonxdata?topic=watsonxdata-cas_ep).\n * `<user-authentication-string>`: The value must be base 64 encoded string of user ID and API key . For more information about the format, see the following note.|
{: caption="Python sample and CURL command" caption-side="bottom"}
{: summary="This table has row and column headers. The row headers identify the service. The column headers identify where that service is located. To understand where a service is located in the table, navigate to the row, and find the for the location you are interested in."}
{: #table07}
{: tab-title="Apache Iceberg"}
{: class="comparison-tab-table"}
{: row-headers}

|Apache Hudi| |
|-----|-----|
| `hudi_demo.py` | The Python Spark application demonstrates the following functionality: \n * It creates a database inside the Apache Hudi catalog (that you created to store data). Here, hudi_db. \n * It creates a table inside the hudi_db database, namely hudi_table. \n * It inserts data into the hudi_table and does SELECT query operation. \n * It drops the table and schema after use. \n  \n Python application :  \n ```\n \n \n       from pyspark.sql import SparkSession\n \n        def init_spark():\n \n            spark = SparkSession.builder \n \n                .appName("CreateHudiTableInCOS") \n \n                .enableHiveSupport() \n \n                .getOrCreate()\n \n            return spark\n \n        def main():\n \n            try:\n \n                spark = init_spark()\n \n                spark.sql("show databases").show()\n \n                spark.sql("create database if not exists spark_catalog.hudi_db LOCATION 's3a://hudi-connector-test/'").show()\n \n                spark.sql("create table if not exists spark_catalog.hudi_db.hudi_table (id bigint, name string, location string) USING HUDI OPTIONS ('primaryKey' 'id', hoodie.write.markers.type= 'direct', hoodie.embed.timeline.server= 'false')").show()\n \n                spark.sql("insert into hudi_db.hudi_table VALUES (1, 'Sam','Kochi'), (2, 'Tom','Bangalore'), (3, 'Bob','Chennai'), (4, 'Alex','Bangalore')").show()\n \n                spark.sql("select * from spark_catalog.hudi_db.hudi_table").show()\n \n                spark.sql("drop table spark_catalog.hudi_db.hudi_table").show()\n \n                spark.sql("drop schema spark_catalog.hudi_db CASCADE").show()\n \n            finally:\n \n                spark.stop()\n \n        if __name__ == '__main__':\n \n            main()\n``` |
| Curl command to submit Python application | ```\n \n    curl --request POST \n \n    --url https://<wxd_host_name>/lakehouse/api/v2/spark_engines/<spark_engine_id>/applications \n \n     --header 'Authorization: Bearer <token>' --header 'Content-Type: application/json' --header 'LhInstanceId: <instance_id>' --data '{ \n \n    "application_details": {\n \n        "conf": {        "spark.serializer" : "org.apache.spark.serializer.KryoSerializer",\n \n        "spark.hadoop.fs.s3a.path.style.access" : "true",\n \n        "spark.hive.metastore.client.plain.username":"ibmlhapikey",\n \n        "spark.hive.metastore.client.plain.password":"<wxd_api_key>",\n \n        "spark.driver.extraJavaOptions" : "-Dcom.sun.jndi.ldap.object.disableEndpointIdentification=true -Djdk.tls.trustNameService=true",\n \n        "spark.executor.extraJavaOptions" : "-Dcom.sun.jndi.ldap.object.disableEndpointIdentification=true -Djdk.tls.trustNameService=true",\n \n        "spark.kryo.registrator": "org.apache.spark.HoodieSparkKryoRegistrar",\n \n        "spark.sql.catalog.spark_catalog.type": "hudi",\n \n        "spark.sql.catalog.spark_catalog": "org.apache.spark.sql.hudi.catalog.HoodieCatalog",\n \n        "spark.hadoop.wxd.cas.endpoint":"<cas_endpoint>/cas/v1/signature",\n \n        "spark.hadoop.wxd.cas.apiKey":"<user-authentication-string>"        },\n \n        "application": "s3a://hudi-connector-test/hudi_demo.py"    }} \n``` |
| Parameter values | Parameter values: \n * `<wxd_host_name>`: The hostname of your watsonx.data Cloud instance. \n * `<instance_id>`: The instance ID from the watsonx.data instance URL. For example, 1609968977179454. \n * `<spark_engine_id>`: The Engine ID of the native Spark engine. \n * `<token>`: The bearer token. For more information about generating the token, see [IAM token](https://test.cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-con-presto-serv#get-ibmiam-token). \n * `<wxd_api_key>`: To generate API key, log in into the watsonx.data console and navigate to Profile > Profile and Settings > API Keys and generate a new API key. \n * `<cas_endpoint>`: The DAS endpoint. To generate DAS endpoint, see [Data Access Service (DAS) endpoint](watsonxdata?topic=watsonxdata-cas_ep). \n * `<user-authentication-string>`: The value must be base 64 encoded string of user ID and API key . For more information about the format, see the following note. |
{: caption="Python sample and CURL command" caption-side="bottom"}
{: summary="This table has row and column headers. The row headers identify the service. The column headers identify where that service is located. To understand where a service is located in the table, navigate to the row, and find the for the location you are interested in."}
{: #table07}
{: tab-title="Apache Hudi"}
{: class="comparison-tab-table"}
{: row-headers}



| Delta Lake | |
|-----|-----|
| `delta_demo.py` | The Python Spark application demonstrates the following functionality: \n * It creates a database inside the Delta Lake catalog (that you created to store data). Here, `iae`.\n * It creates a table inside the `iae` database, namely `employee`. \n * It inserts data into the `employee` and does SELECT query operation.\n * It drops the table and schema after use. \n \n Python application : ```\n \n    from pyspark.sql import SparkSession \n \n      import os\    def init_spark(): \n \n         spark = SparkSession.builder.appName("lh-hms-cloud")\n \n         .enableHiveSupport().getOrCreate()\n \n        return spark\n \n    def main():\n \n        spark = init_spark()\n \n        spark.sql("show databases").show()\n \n        spark.sql("create database if not exists spark_catalog.iae LOCATION 's3a://delta-connector-test/'").show()\n \n        spark.sql("create table if not exists spark_catalog.iae.employee (id bigint, name string, location string) USING DELTA").show()\n \n        spark.sql("insert into spark_catalog.iae.employee VALUES (1, 'Sam','Kochi'), (2, 'Tom','Bangalore'), (3, 'Bob','Chennai'), (4, 'Alex','Bangalore')").show()\n \n        spark.sql("select * from spark_catalog.iae.employee").show()\n \n        spark.sql("drop table spark_catalog.iae.employee").show()\n \n        spark.sql("drop schema spark_catalog.iae CASCADE").show()\n \n        spark.stop()\n \n    if __name__ == '__main__':\n \n        main()\n``` |
| Curl command to submit Python application| ```\n \n    curl --request POST \n \n    --url https://<wxd_host_name>/lakehouse/api/v2/spark_engines/<spark_engine_id>/applications \n \n    --header 'Authorization: Bearer <token>' \n \n    --header 'Content-Type: application/json' \n \n    --header 'LhInstanceId: <instance_id>' \n \n    --data '{        "application_details": {\n \n        "conf": {\n \n                "spark.sql.catalog.spark_catalog" : "org.apache.spark.sql.delta.catalog.DeltaCatalog",\n \n                "spark.sql.catalog.spark_catalog.type" : "hive",\n \n                "spark.hive.metastore.client.plain.username" : "ibmlhapikey",\n \n                "spark.hive.metastore.client.plain.password" : "<wxd_api_key>",\n \n                "spark.hadoop.wxd.cas.endpoint":"<cas_endpoint>/cas/v1/signature",                "spark.hadoop.wxd.cas.apiKey":"base64 encoding(ibmlhapikey_<username>:<user_apikey>)"        },\n \n        "application": "s3a://delta-connector-test/delta_demo.py"        }    }\n``` |
| Parameter values | Parameter values: \n * `<wxd_host_name>`: The hostname of your watsonx.data Cloud instance. \n * `<instance_id>` : The instance ID from the watsonx.data cluster instance URL. For example, 1609968977179454. \n * `<spark_engine_id>` : The Engine ID of the native Spark engine. \n * `<token>` : The bearer token. For more information about generating the token, see [IAM token](https://test.cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-con-presto-serv#get-ibmiam-token). \n * `<wxd_api_key>`: To generate API key, log in into the watsonx.data console and navigate to Profile > Profile and Settings > API Keys and generate a new API key. \n * `<cas_endpoint>`: The DAS endpoint. To generate DAS endpoint, see [Data Access Service (DAS) endpoint](watsonxdata?topic=watsonxdata-cas_ep). \n * `<user-authentication-string>`: The value must be base 64 encoded string of user ID and API key . For more information about the format, see the following note. |
{: caption="Python sample and CURL command" caption-side="bottom"}
{: summary="This table has row and column headers. The row headers identify the service. The column headers identify where that service is located. To understand where a service is located in the table, navigate to the row, and find the for the location you are interested in."}
{: #table07}
{: tab-title="Delta Lake"}
{: class="comparison-tab-table"}
{: row-headers}

The value of `<user-authentication-string>` must be in the format `echo -n '<user>:<apikey>' | base64`.  Here, `<user_id>` is the IBM Cloud ID of the user whose apikey is used to access the data bucket. The `<IAM_APIKEY>` here is the API key of the user accessing the Object store bucket. To generate API key, log in into the watsonx.data console and navigate to Profile > Profile and Settings > API Keys and generate a new API key. If you generate a new API key, your old API key becomes invalid.
{: important}

8. After you submit the Spark application, you receive a confirmation message with the application ID and Spark version. Save it for reference.
9. Log in to the watsonx.data cluster, access the Engine details page. In the Applications tab, use application ID to list the application and track the stages. For more information, see [View and manage applications](watsonxdata?topic=watsonxdata-mng_appltn).

| Column 1 | Column 2 | Column 3 |
|----------|---------|---------|
| Cell | Cell | Cell |
| Cell |      | Cell |
| Cell | Cell | Cell |
{: caption="ADD TABLE CAPTION HERE" caption-side="bottom"}
{: tab-title="Tab 1"}
{: tab-group="simple-tab-group"}
{: class="simple-tab-table"}
{: #simpletabtable1}

| Column 1 | Column 2 | Column 3 |
|----------|---------|---------|
|      | Cell | Cell |
| Cell | Cell | Cell |
| Cell | Cell |      |
{: caption="ADD ANOTHER TABLE CAPTION HERE" caption-side="bottom"}
{: tab-title="Tab 2"}
{: tab-group="simple-tab-group"}
{: class="simple-tab-table"}
{: #simpletabtable2}



    | Column 1 | Column 2 | Column 3 |
    |----------|---------|---------|
    | Cell | Cell | Cell |
    | Cell |      | Cell |
    | Cell | Cell | Cell |
    {: caption="ADD TABLE CAPTION HERE" caption-side="bottom"}
    {: tab-title="Tab 1"}
    {: tab-group="simple-tab-group"}
    {: class="simple-tab-table"}
    {: #simpletabtable1}

    | Column 1 | Column 2 | Column 3 |
    |----------|---------|---------|
    |      | Cell | Cell |
    | Cell | Cell | Cell |
    | Cell | Cell |      |
    {: caption="ADD ANOTHER TABLE CAPTION HERE" caption-side="bottom"}
    {: tab-title="Tab 2"}
    {: tab-group="simple-tab-group"}
    {: class="simple-tab-table"}
    {: #simpletabtable2}
