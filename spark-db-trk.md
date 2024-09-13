---

copyright:
  years: 2024
lastupdated: "2024-09-13"
keywords: spark, interface
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Track Spark applications
{: #db_trk}

You can track your Spark applications by using Databand through the methods that are mentioned in this section.

## Databand listener
{: #db_listen}

This method automatically tracks dataset operations. With an agent, you can activate Databand listeners without incorporating them into your project or making further code modifications. The agent's `FatJar` (`-all.jar` file) includes all necessary Databand code. You can specify this jar dependency when submitting your Spark applications. Download the latest version of the jar from [Maven Repository](https://repo1.maven.org/maven2/ai/databand/dbnd-agent/).

## Databand decorators and logging API
{: #db_api}

This approach enables manual tracking, allowing Databand to provide insights into your code errors, metrics, and logging details. To use this method, you must import the `dbnd` module, which requires code modifications.

A library set is a collection of libraries that you create and use in Spark applications. To install the `dbnd` package and create a custom library set for use in Spark applications, you can use the Spark application `customize_instance_app.py` provided by {{site.data.keyword.lakehouse_short}}.
Do the following steps to install `dbnd` package:

1. Prepare a JSON file as follows:

   ```json
   {
     "library_set": {
       "action": "add",
       "name": "dbnd-lib",
       "libraries": {
         "pip": {
           "python": {
             "packages": [
               "dbnd"
             ]
           }
         }
       }
     }
   }
   ```
   {: codeblock}

   The following are the JSON attributes:

   - **`library_set`**: The top-level JSON object that defines the library set.
   - **`action`**: Specifies the action to be taken for the library set. To create a library set, you use `add`. Currently, `add` is the only option supported.
   - **`name`**: Specifies the name with which the library set is identified. The created library set is stored in a file with this name in the IBM Cloud Object Storage instance that you specified as instance home.
   - **`libraries`**: Defines a set of libraries.
   - **`conda`**: Library package manager.
   - **`python`**: The library language. Currently, only Python is supported.
   - **`packages`**: List of packages to install. To install a specific version of a package, pass the version by using the format `package_name==version`.

1. Pass the JSON file as arguments in the following REST API call. Make sure that you escape the quotes as required while passing to the REST API call.

   *Example: `submit-application.json`*

   ```json
   {
     "application_details": {
       "application": "/opt/ibm/customization-scripts/customize_instance_app.py",
       "arguments": [
         "{\"library_set\":{\"action\":\"add\",\"name\":\"dbnd-lib\",\"libraries\":{\"pip\":{\"python\":{\"packages\": [\"dbnd\"]}}}}}"
       ]
     }
   }
   ```
   {: codeblock}

1. Submit the Spark application to the Spark engine by using the following curl command.

   ```bash
   curl --request POST \
     --url https://<region>.lakehouse.cloud.ibm.com/lakehouse/api/v2/spark_engines/<spark_engine_id>/applications \
     --header 'Authorization: Bearer <token>' \
     --header 'Content-Type: application/json' \
     --header 'AuthInstanceID: <crn_instance>' \
     --data @submit-application.json
   ```
   {: codeblock}

   Following are the parameter values:

   - **`region`**: The region where the Spark instance is provisioned.
   - **`<spark_engine_id>`**: The Engine ID of the native Spark engine.
   - **`token`**: The bearer token. For more information about generating the token, see [Generating a bearer token](https://cloud.ibm.com/apidocs/watsonxdata#authentication).
   - **`<crn_instance>`**: The CRN of the {{site.data.keyword.lakehouse_short}} instance.

1. If the application is accepted, you receive a response as follows:

   ```bash
   {
     "id": "87e63712-a823-4aa1-9f6e-7291d4e5a113",
     "state": "accepted"
   }
   ```
   {: screen}

   When the `state` turns to **FINISHED**, the library set creation is complete.

For more information See [Creating a library set for Python package install](https://cloud.ibm.com/docs/AnalyticsEngine?topic=AnalyticsEngine-create-lib-set).
