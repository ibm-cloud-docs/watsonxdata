---

copyright:
  years: 2022, 2025
lastupdated: "2025-09-11"

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

   **Sample V2 API**

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


   **Sample V3 API**

    ```sh
    curl -X POST https://<region>.lakehouse.cloud.ibm.com/lakehouse/api/v3/spark_engines/<spark_engine_id>/applications --header "Authorization: Bearer <IAM token>" -H "content-type: application/json"  -d @submit-spark-app.json
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


## Using the library set created using script based customization
{: #script-cust-using1}

When you use a library set that you created using a script, you need to include the path of the library in certain environment variables so that the library set can be accessed by your Spark application.

For example, if your custom library is a `.so` file, you need to add `"EXTRA_LD_LIBRARY_PATH"` to the `"env"` section of the Spark application submit call, with the value `/home/spark/shared/user-libs/<libraryset_name>/custom/<subdir_if_applicable>`. This prepends `"EXTRA_LD_LIBRARY_PATH"` to `"LD_LIBRARY_PATH"`, ensuring that this is the first path to the `.so` file that is searched.


If your custom library is a JAR file and you need it to be accessible on the Spark classpath, you must specify the JAR file in the extra classpath for driver/executor depending on where you require the JAR file. For example, to add it in front of the driver classpath, add the following property, where the library set name is `java_library`:

```bash
"spark.driver.extraClassPath":"/home/spark/shared/user-libs/java_library/custom/*"
```

If your custom library is a certificate file, for example a self signed ICD Postgres certificate, you can specify it in the connection URL in the following way:
```bash
sslrootcert=/home/spark/shared/user-libs/customize_integration_custom_lib/custom/postgres.cert`
```


If your custom library is a configuration file, it is made available to the Spark drivers and executors automatically.

## Example of customization script with a multi file download
{: #cust-multi-file-download1}

The parameters, and the script mentioned in the previous section are just a sample. You can implement additional logic if you need, like for downloading a directory or multiple files or downloading from different source, and so on.

For example, to download multiple files from a directory on Cloud Object Storage, see [Sample script](https://github.com/IBM-Cloud/IBM-Analytics-Engine/tree/master/ae-serverless/customization/multi-file-libraryset-example).
