---

copyright:
  years: 2017, 2025
lastupdated: "2025-02-24"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Submitting Spark application from Console
{: #smbit_cnsl_1}

You can submit a Spark application that is written in Python, Java, or Scala language from the {{site.data.keyword.lakehouse_short}} Console on IBM Cloud.

It is possible to specify the Spark application details, version to be considered, hardware and volume details, Spark environment properties and Spark configurations in the {{site.data.keyword.lakehouse_short}} Console.



## Prerequisites
{: #nsppk_cnsl_2}


Your Spark application must be available in an accessible storage.


## Procedure
{: #sppk_cnsl_3}

1. Log in to the {{site.data.keyword.lakehouse_short}} instance. Go to the **Infrastructure manager** page.
2. Click the name of Spark engine (either from list or topology view). Engine information window opens.
3. In the **Applications** tab, click the **Create application** button. The Submit Spark application page opens.
   a. Select the **Inputs** tab. Configure the following details:

      | Field | Description |
      | --- | --- |
      | Application type | You have the following option: \n - Python: If your Spark application is written in Python language, select this option.\n  - Java or Scala: If your Spark application is written in Java or Scala language, select this option. |
      | Application path | Specify the path to your application. This is a mandatory field. \n Example: s3a://<application-bucket-name>/iceberg.py |
      | Application name | Specify a name for the application. |
      | Arguments | Use the Add argument button to specify all arguments required by the application. |
      | Spark version | Enter the Spark version for running your application. Spark 3.4 and 3.5 are the versions available. |
      | Spark configuration properties | Specify the Spark properties in the form of key-value pair ("<property_name>": "<property_value>") separated by comma. For more information about the different properties, see [Properties](https://spark.apache.org/docs/latest/configuration.html#available-properties). |
      | Spark environment properties | Specify the Spark environment properties as key=value pairs. For more information about the different properties, see [Environment properties](https://spark.apache.org/docs/latest/configuration.html#runtime-environment). |
      | Hardware configuration | Specify the number of CPU cores (Driver and Executor) and memory that is required for the workload. |
      | Volume | Specify the details of IBM Storage Hub volume that should be mounted for your Spark application. Click Add volume link to add details of each volume. |
      | Mount Path | The Spark application nodes where the volume is mounted. The files in the volume, which is referenced in your application script must have path relative to the Mount path. |
      | Source sub path | To mount only a specific directory in the volume, specify the path here. |
      | Dependencies | You can specify the path to the dependent files. |
      | Import from payload | Click this link to automatically import and furnish all fields under the Inputs tab if you have already specified the payload in the **Payload** tab. |
      {: caption="Configuration details " caption-side="bottom"}

4. Select the **Payload** tab.

      In the **Application payload** field, specify the application payload JSON that can be accepted by the Spark engine application creation REST API endpoint. You can either manually write the payload here or click the **Import from inputs** link to automatically build the JSON from the details provided in the **Inputs** tab.

4. Click **Submit application**. The application is successfully submitted and gets listed under the **Applications** tab.
