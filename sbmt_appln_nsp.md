---

copyright:
  years: 2017, 2024
lastupdated: "2024-08-23"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Submitting Spark application by using native Spark engine
{: #smbit_nsp}


## Prerequisites
{: #nsppk_preq}

To enable your Spark application to work with the watsonx.data catalog and storage, you must have `Metastore admin` role. Without `Metastore admin` privilege, you cannot ingest data to storage using Native Spark engine. For more information about the Spark configuration, see [Working with the watsonx.data catalog and storage](#view_smbit_nsp).



You can submit a Spark application by running a CURL command. Complete the following steps to submit a Python application.

1. Create an object storage to store the Spark application and related output. To create Cloud Object Storage and a bucket, see [Creating a storage bucket](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-secure-content-store#create-cos-bucket). You must maintain separate storage for application and data. You must register only data buckets with {{site.data.keyword.lakehouse_short}}.
2. Register the Cloud Object Storage in {{site.data.keyword.lakehouse_short}}, register Cloud Object Storage bucket. To register Cloud Object Storage bucket, see [Adding bucket catalog pair](watsonxdata?topic=watsonxdata-reg_bucket).

    You can create different Cloud Object Storage buckets to store application code and the output. You must register the data bucket which stores the input data, and watsonx.data tables. You need not register the storage bucket which maintains the application code with watsonx.data.
    {: note}

3. Upload the Spark application to the Cloud Object Storage application bucket, see [Uploading data](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-secure-content-store#upload-data).
4. Run the following curl command to submit the word count application.

    Example 1:


    ```bash
    curl --request POST \
      --url https://<region>.lakehouse.cloud.ibm.com/lakehouse/api/v2/spark_engines/<spark_engine_id>/applications \
      --header 'Authorization: Bearer <token>' \
      --header 'Content-Type: application/json' \
      --header 'AuthInstanceID: <crn_instance>' \
      --data '{
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

    Example 2:

    Run the following curl command to customize the cluster hardware sizes:


    ```bash
    curl -k -X POST \
    --url https://<region>.lakehouse.cloud.ibm.com/lakehouse/api/v2/spark_engines/<spark_engine_id>/applications \
    --header 'Authorization: Bearer <token>' \
    --header 'Content-Type: application/json' \
    --header 'AuthInstanceID: <crn_instance>' \
    -d '{
        "application_details": {
            "application": "/opt/ibm/spark/examples/jars/spark-examples*.jar",
            "arguments": ["1"],
            "class": "org.apache.spark.examples.SparkPi",
            "conf": {
                "spark.driver.memory": "4G",
                "spark.driver.cores": 1,
                "spark.executor.memory": "4G",
                "spark.executor.cores": 1,
                "ae.spark.executor.count": 1
            }
        }
    }'
    ```
    {: codeblock}

5. If your Spark application resides in Cloud Object Storage, specify the parameter values and run the following curl command. The following example shows the command to submit read.py application.

    Example 3:
    ```bash
    curl --request POST \
      --url https://<region>.lakehouse.cloud.ibm.com/lakehouse/api/v2/spark_engines/<spark_engine_id>/applications \
      --header 'Authorization: Bearer <token>' \
      --header 'Content-Type: application/json' \
      --header 'AuthInstanceID: <crn_instance>' \
      --data '{
      "application_details": {
        "application": "s3a://<s3_bucket_name>/cos-read.py",
        "conf": {
            "spark.hadoop.fs.s3a.bucket.<s3_bucket_name>.endpoint": "<cos_endpoint>",
            "spark.hadoop.fs.s3a.bucket.<s3_bucket_name>.access.key": "<s3 bucket HMAC access key>",
            "spark.hadoop.fs.s3a.bucket.<s3_bucket_name>.secret.key": "<s3 bucket  HMAC secret key>",
            "spark.app.name": "reader-app"
        }
      }
    }'
    ```
    {: codeblock}


   Parameter values:
   * `<region>`: The region where the Spark instance is provisioned.
   * `<spark_engine_id>` : The Engine ID of the native Spark engine.
   * `<token>` : The bearer token. For more information about generating the token, see [Generating a bearer token](https://cloud.ibm.com/apidocs/watsonxdata#authentication).
   * `<crn_instance>` : The CRN of the watsonx.data instance.
   * `<bucket_name>` : The name of the object storage. Object storage can be Amazon S3, Ceph, Hadoop Distributed File System (HDFS) or IBM Cloud Object Storage (COS). For more information, see [Adding a storage-catalog pair](watsonxdata?topic=watsonxdata-reg_bucket).
   * `<cos_endpoint>`: The direct endpoint of the Object Storage bucket. For example, s3.direct.us-south.cloud-object-storage.appdomain.cloud.
   * `<s3 bucket HMAC access key>` : The access key for object storage. For more information, see [Create HMAC credentials using the CLI](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-uhc-hmac-credentials-main#uhc-create-hmac-credentials-cli).
   * `<s3 bucket HMAC secret key>` : The secret key for object storage. For more information, see [Create HMAC credentials using the CLI](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-uhc-hmac-credentials-main#uhc-create-hmac-credentials-cli).



6. After you submit the Spark application, you receive a confirmation message with the application ID and Spark version. Save it for reference.
7. Log in to the watsonx.data cluster, access the **Engine details** page. In the **Applications** tab, use the application ID to list the application and you can track the stages. For more information, see [View and manage applications](watsonxdata?topic=watsonxdata-mng_appltn).


## Working with the watsonx.data catalog and storage
{: #view_smbit_nsp}

To enable your Spark application to work with the watsonx.data catalog and storage, add the following configuration to your application payload:

```bash
spark.hadoop.wxd.apiKey=Basic <base64value>
```
{: codeblock}

The username is by default `ibmlhapikey` and `<base64value>` is derieved using the following command

```bash
 echo -n "ibmlhapikey_<ibmcloudid>:<apikey>" | base64
```
{: codeblock}
