---

copyright:
  years: 2022, 2024
lastupdated: "2024-09-13"

keywords: watsonxdata, qhmm

subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Creating a library set for other packages or file download
{: #cust-script1}

If you want to customize your instance by adding libraries to a library set that you fetch from sources other than through the `conda` or `pip` repositories, you should use script based customization.
{: shortdesc}


With script based customization, you create a Python script using the module naming convention expected by {{site.data.keyword.lakehouse_short}}. Also, you need to implement a Python function that acts as the executable entry point to your script. In this script, you can add your own logic for downloading the libraries and placing them in a predesignated directory, which is `/home/spark/shared/user-libs/<libraryset_name>/custom/<subdir_if_applicable>`, so that they become part of the library set and get stored for later consumption in your application.

## Creating a library set using script based customization
{: #lib-set-script-cust1}

Perform these steps to create a library set using script based customization:
1. Create a Python file named `customization_script.py`. {{site.data.keyword.lakehouse_short}}'s customization component looks for a Python module with this name.
1. In your `customization_script.py`, implement a function called `customize(<install_path>, <params>)`, where `<install_path>` is the predesignated location where the libraries are downloaded to, namely `/home/spark/shared/user-libs/<libraryset_name>/custom/<subdir_if_applicable>`. You can't change this path. `<params>` is a list of the parameters required by the customization script.
1. Store the `customization_script.py` file in {{site.data.keyword.cos_full_notm}} or in GitHub.
1. Pass the location of the `customization_script.py` file to the customization Spark application through the `"application_details" > "conf" > "spark.submit.pyFiles"` parameter.

    The `"arguments"` section in the Spark application submission payload must contain a `"library_set"` section with details, like `"action"` and `"name"` as shown in the following sample payload.

    Example of the payload:
    ```json
    {
      "application_details": {
      "application": "/opt/ibm/customization-scripts/customize_instance_app.py",
        "arguments": ["{\"library_set\":{\"action\":\"add\",\"name\":\"customize_integration_custom_lib\",\"script\":{\"source\":\"py_files\",\"params\":[\"https://s3.direct.<CHANGEME_REGION>.cloud-object-storage.appdomain.cloud\",\"<CHANGEME_BUCKET_NAME>\",\"libcalc.so\",\"<CHANGEME_ACCESS_KEY>\",\"<CHANGEME_SECRET_KEY>\"]}}}"],
        "conf": {
          "spark.hadoop.fs.cos.dev-cos.endpoint":"https://s3.direct.<CHANGEME_REGION>.cloud-object-storage.appdomain.cloud",
          "spark.hadoop.fs.cos.dev-cos.access.key":"<CHANGEME_ACCESS_KEY>",
          "spark.hadoop.fs.cos.dev-cos.secret.key":"<CHANGEME_SECRET_KEY>",
          "spark.submit.pyFiles":"cos://<CHANGEME_BUCKET_NAME>.dev-cos/customization_script.py"
        }
      }
    }
    ```
    {: codeblock}

    Example of customization_script.py:
    ```python
    import cos_utils
    import os
    import sys

    def customize(install_path, params):
      print ("inside base install_misc_package(), override this to implement your own implementation.")
      for param in params:
       print(param)
      endpoint = params[0]
      bucket_name = params[1]
      log_config_file = params[2]
      access_key = params[3]
      secret_key = params[4]
      cos = cos_utils.get_cos_object(access_key, secret_key, endpoint)

      retCode = cos_utils.download_file(log_config_file, cos, bucket_name, "{}/{}".format(install_path, log_config_file))
      if (retCode != 0):
           print("non-zero return code while downloading file    {}".format(str(retCode)))
           sys.exit(retCode)
      else:
           print("Successfully downloaded file...")
    ```
    {: codeblock}

    To run the application, use the following command.

    ```sh
    curl --request POST
        --url https://<region>.lakehouse.cloud.ibm.com/lakehouse/api/v2/spark_engines/<spark_engine_id>/applications
        --header 'Authorization: Bearer <token>'
        --header 'Content-Type: application/json'
        --header 'AuthInstanceID: <crn_instance>'
        -d @createLibraryset.json
    ```
    {: codeblock}


    Parameter values:
    * `<region>` : The region where the Spark instance is provisioned.
    * `<spark_engine_id>` : The Engine ID of the native Spark engine.
    * `<crn_instance>` : The CRN of the watsonx.data instance.
    * `<token>` : The bearer token. For more information about generating the token, see [Generating a bearer token](https://cloud.ibm.com/apidocs/watsonxdata#authentication).

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
