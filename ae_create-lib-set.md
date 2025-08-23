---

copyright:
  years: 2022, 2025
lastupdated: "2025-08-23"

keywords: watsonxdata, qhmm

subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Creating a library set for Python package install
{: #create-lib-set1}

A library set is a collection of libraries that you can create and reference in Spark applications that consume the libraries. The library set is stored in the instance home storage associated with the instance at the time the instance is created.
{: shortdesc}

If you want to customize your instance by adding libraries to a library set that you fetch from sources other than through the `conda` or `pip` repositories, you should use one of the following:


* [Creating a library set for Python package install](#create-lib-se1)
* [Creating a library set for other packages or file download (Script based)](#create-lib-se2)

## Creating a library set for Python package install
{: #create-lib-se1}

Currently, you can only install Python packages through `conda` or `pip install`.
Spark engine bundles a Spark application called `customize_instance_app.py` that you run to create a library set with your custom packages and can be consumed by your Spark applications.

**Prerequites**: To create a library set, you must have the permissions to submit a Spark application. See [Managing roles and privileges](/docs/watsonxdata?topic=watsonxdata-role_priv).

To create a library set:

1. Prepare a JSON file like the following:
    ```json
    {
      "library_set": {
        "action": "add",
        "name": "my_library_set",
        "libraries": {
          "conda": {
            "python": {
              "packages": ["numpy"]
              }
          }
      }
      }
    }
    ```
    {: codeblock}

    The description of the JSON attributes are as follows:
    - `"library_set"`: The top level JSON object that defines the library set.
    - `"action"`: Specifies the action to be taken for the library set. To create a library set, we use `"add"`. Currently, `"add"` is the only option supported.
    - `"name"`: Specifies the name with which the library set is identified. The created library set is stored in a file with this name in the {{site.data.keyword.cos_full_notm}} instance that you specified as `instance home`. **Important**: If you create more than one library set, you must use unique names for each set. Otherwise they will overwrite one another.
    - `"libraries"`: Defines a set of libraries. You can specify one or more libraries in this section. This element has one child JSON object per library package manager. Currently, only the `"conda"` and `"pip"` package managers are supported. Use `"pip"` or `"conda"` to install Python packages.
    - `"conda"`: Library package manager.
    - `"python"`: The library language. Currently, only Python is supported.
    - `"packages"`: List of packages to install. To install a specific version of a package, pass the version using this format: `package_name==version`.

1. Get the [IAM token](/docs/AnalyticsEngine?topic=AnalyticsEngine-retrieve-iam-token-serverless).
1. Pass the JSON file as `"arguments"` in the following REST API call. Make sure that you escape the quotes as required, while passing to the REST API call.
    ```sh
    curl --request POST
        --url https://<region>.lakehouse.cloud.ibm.com/lakehouse/api/v2/spark_engines/<spark_engine_id>/applications
        --header 'Authorization: Bearer <token>'
        --header 'Content-Type: application/json'
        --header 'AuthInstanceID: <crn_instance>'
        -d @createLibraryset.json
    ```
    {: codeblock}

    **Important**: You must escape all double quote characters in the strings that are passed as application arguments.


    Parameter values:
    * `<region>` : The region where the Spark instance is provisioned.
    * `<spark_engine_id>` : The Engine ID of the native Spark engine.
    * `<crn_instance>` : The CRN of the watsonx.data instance.
    * `<token>` : The bearer token. For more information about generating the token, see [Generating a bearer token](https://cloud.ibm.com/apidocs/watsonxdata#authentication).

   ** Example payload**:


    ```bash
        --url https://<region>.lakehouse.cloud.ibm.com/lakehouse/api/v2/spark_engines/<spark_engine_id>/applications
        --header 'Authorization: Bearer <token>'
        --header 'Content-Type: application/json'
        --header 'AuthInstanceID: <crn_instance>'
        -d '{
        "application_details": {
                "application": "/opt/ibm/customization-scripts/customize_instance_app.py",
                "arguments": ["{
      "library_set": {
        "action": "add",
        "name": "my_library_set",
        "libraries": {
          "conda": {
            "python": {
              "packages": ["numpy"]
              }
          }
      }
      }
    }"]
       }
  }'
    ```
    {: codeblock}


    If the application is accepted, you will receive a response like the following:
    ```json
    {
      "id": "87e63712-a823-4aa1-9f6e-7291d4e5a113",
      "state": "accepted"
    }
    ```

    When the state turns to FINISHED, the library set creation is complete.
1. Track the status of the application by invoking the application status REST API.


## Creating a library set for other packages or file download (Script based)
{: #create-lib-se2}


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
