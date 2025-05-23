---

copyright:
  years: 2022, 2025
lastupdated: "2025-03-24"

keywords: watsonxdata, qhmm

subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Creating a library set for Python package install
{: #create-lib-set1}

A library set is a collection of libraries that you can create and reference in Spark applications that consume the libraries. The library set is stored in the instance home storage associated with the instance at the time the instance is created.

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

    If the application is accepted, you will receive a response like the following:
    ```json
    {
      "id": "87e63712-a823-4aa1-9f6e-7291d4e5a113",
      "state": "accepted"
    }
    ```

    When the state turns to FINISHED, the library set creation is complete.
1. Track the status of the application by invoking the application status REST API.
