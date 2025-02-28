---

copyright:
  years: 2017, 2024
lastupdated: "2025-02-07"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# View and edit Native Spark engine details
{: #view_edit}

You can use the {{site.data.keyword.lakehouse_full}} UI or API to view and edit the Native Spark details.

## Viewing Native Spark engine details
{: #view_nspark}

You can view the Native Spark engine details in list and topology views.

1. Log in to the {{site.data.keyword.lakehouse_short}} cluster and go to the **Infrastructure manager** page.
1. Click on the name of the Spark engine (either from list or topology view). The **Engine information** window opens.
1. In the **Details** tab, you can view the following details:

   | Field | Description |
   |-------------|-------------|
   | Display name | The Spark engine name. |
   | Engine ID | The unique identifier of the Spark instance. |
   | Description | The description of the engine. |
   | Tags | The tag that is specified at the time of registering an engine. |
   | Default Spark version | The Spark runtime version that is used by default for any application that is submitted to the Spark engine. |
   | Engine Home bucket | Specify the bucket name that store the events and logs related to Spark. |
   | Type | The engine type (here, Spark). |
   | {{site.data.keyword.lakehouse_short}} application endpoint | The endpoint is used at the time of application submission. To submit an application by using API, see [API Docs][def2]. |
   | Spark engine endpoint | The Native Spark endpoint. |
   | Default Spark Configuration | The Spark configuration properties that are applied to any application that is submitted to the Spark engine. |
   {: caption="Viewing Native Spark engine details" caption-side="bottom"}

## Editing Spark details from the console UI
{: #edit_nspark_ui}

You can edit the Spark details in list and topology views.

1. Log in to the {{site.data.keyword.lakehouse_short}} cluster and go to the **Infrastructure manager** page.
1. Click the name of the Spark engine (either from list or topology view). The **Engine information** window opens.
1. In the **Details** tab, click **Edit**.
1. In the **Display name** field, enter the display name for the Spark engine.
1. In the **Description** field, enter the description of the engine or edit the existing description.
1. In the **Tags** field, select the tags from the list or start typing to define a new tag.
1. In the **Default Spark version** field, select the Spark runtime version that must be considered for processing the applications.
1. In the **Default Spark configuration** field, click **Edit configuration** link to update the default Spark configuration. For more information about different properties, see [Available Properties][def].
   1. Enter the key-value pair for the Spark configuration that applies to all applications.
   1. Click **Apply**.
1. Click **Save** and click the name of the Spark engine (either from list or topology view). The **Engine information** window opens.

## Editing Spark details by using API
{: #edit_nspark_api}

Use the following curl to update the Spark engine details like tags, description, default configuration, and Spark version.

```bash
   curl --request PATCH \
     --url https://<region>.lakehouse.cloud.ibm.com/lakehouse/api/v2/spark_engines/<spark_engine_id> \
     --header 'Authorization: Bearer <token>' \
     --header 'Content-Type: application/merge-patch+json' \
     --header 'AuthInstanceID: <crn_instance>' \
     --data '{
     "engine_details": {
       "default_config": <map_of_spark_properties>,
       "default_version": "<spark_version>"
     }
   }'
```
{: codeblock}

Following are the details of the parameter values to be used in the curl command:

| Parameter | Description |
| --- | --- |
| `<region>` | The region of the provisioned Spark instance. |
| `<spark_engine_id>` | The engine ID of the native Spark engine. |
| `<token>` | The bearer token. For more information about generating the token, see [Generating a bearer token][def5]. |
| `<crn_instance>` | The CRN of the {{site.data.keyword.lakehouse_short}} instance. |
| `<map_of_spark_properties>` | Specify the Spark properties in the form of key-value pair (`"<property_name>": "<property_value>"`) separated by comma. |
| `<property_name>` | The default configuration property name. For more information about different properties, see [Available Properties][def6]. |
| `<property_value>` | The value that must be configured for the property. For more information about different properties, see [Available Properties][def6]. |
| `<spark_version>` | The Spark runtime. To know about supported Spark versions, see [Supported Spark version](watsonxdata?topic=watsonxdata-wxd-ae_limits#cpu-mem-spk_versn). |
{: caption="Parameter list" caption-side="bottom"}

**Example**:
```bash
   curl --request PATCH \
     --url https://<region>.lakehouse.cloud.ibm.com/lakehouse/api/v2/spark_engines/<spark_engine_id> \
     --header 'Authorization: Bearer <token>' \
     --header 'Content-Type: application/merge-patch+json' \
     --header 'AuthInstanceID: <crn_instance>' \
     --data '{
     "engine_details": {
       "default_config": {
         "spark.driver.cores": "1",
         "spark.driver.memory": "4g"
       },
       "default_version": "3.4"
     }
   }'
```
{: codeblock}

To add new properties to the `default_config` parameter or to update existing properties, specify the property name and value. To delete a property, specify the property name and the set the value to `NULL`.
{: note}

[def]: https://spark.apache.org/docs/latest/configuration.html#available-properties
[def2]: https://cloud.ibm.com/apidocs/watsonxdata-software#create-spark-engine-application
[def5]: https://cloud.ibm.com/apidocs/watsonxdata#authentication
[def6]: https://spark.apache.org/docs/latest/configuration.html#available-properties

## Related API
{: #viewspark_api}

For information on related API, see
* [List all spark engines](https://cloud.ibm.com/apidocs/watsonxdata#list-spark-engines)
* [Get spark engine](https://cloud.ibm.com/apidocs/watsonxdata#get-spark-engine)
* [Update spark engine](https://cloud.ibm.com/apidocs/watsonxdata#update-spark-engine)
