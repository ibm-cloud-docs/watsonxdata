---

copyright:
  years: 2022, 2025
lastupdated: "2025-03-24"

keywords: watsonx.data, spark, analytics, configuring
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Using a library set
{: #use-lib-set-1}

After you have created a library set, you can reference and consume it in your Spark applications. When you run your Spark application in the {{site.data.keyword.lakehouse_short}} instance, the library set is loaded from the instance home and is made available to the Spark application.


A library set is referenced in a Spark application using the `"ae.spark.librarysets"` parameter in the `"conf"` section of the Spark application submission payload.

To reference a library set when submitting a Spark application:

1. Get the IAM token. See [Generating a bearer token](https://cloud.ibm.com/apidocs/watsonxdata#authentication).
1. Issue the following cURL command:
    ```sh
    curl -X POST https://<region>.lakehouse.cloud.ibm.com/lakehouse/api/v2/spark_engines/<spark_engine_id>/applications --header "Authorization: Bearer <IAM token>" -H "content-type: application/json"  -d @submit-spark-app.json
    ```
    {: codeblock}

    Example for submit-spark-app.json:
    ```json
    {
      "application_details": {
      "application": "cos://<bucket-name>.<cos-name>/my_spark_application.py",
      "arguments": ["arg1", "arg2"],
      "conf": {
        "spark.hadoop.fs.cos.<cos-name>.endpoint":"https://s3.us-south.cloud-object-storage.appdomain.cloud",
        "spark.hadoop.fs.cos.<cos-name>.access.key":"<access_key>",
        "spark.hadoop.fs.cos.<cos-name>.secret.key":"<secret_key>",
        "ae.spark.librarysets":"my_library_set"
        }
    }
    }
    ```
    {: codeblock}


    Currently, only one library set can be referenced during Spark application submission under the `"ae.spark.librarysets"` attribute.
    {: note}

    If the application is accepted, you will receive a response like the following:
    ```json
    {
      "id": "87e63712-a823-4aa1-9f6e-7291d4e5a113",
      "state": "accepted"
    }
    ```

1. Track the status of the application by invoking the application status REST API. See [View and manage applications](/docs/watsonxdata?topic=watsonxdata-mng_appltn).
