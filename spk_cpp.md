---

copyright:
  years: 2022, 2025
lastupdated: "2025-08-23"

keywords: lakehouse, watsonx.data, query optimizer, install

subcollection: watsonxdata

---

{:javascript: #javascript .ph data-hd-programlang='javascript'}
{:java: #java .ph data-hd-programlang='java'}
{:ruby: #ruby .ph data-hd-programlang='ruby'}
{:php: #php .ph data-hd-programlang='php'}
{:python: #python .ph data-hd-programlang='python'}
{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:video: .video}

# Provisioning Gluten accelerated Spark engine
{: #prov_cpp}

Gluten accelerated Spark engine is an optimized, high-performance engine in {{site.data.keyword.lakehouse_short}}. The Spark engine uses Gluten for offloading SQL execution to Velox, which is an open source execution engine(implemented in C++) thereby accelerating the computation of SparkSQL to reduce the cost for running the workloads.


## Provisioning Gluten accelerated Spark engine
{: #prov_cpp_1}

**Applies to** :  [Gluten accelerated Spark engine]{: tag-green}

IBM watsonx.data allows you to provision a Gluten accelerated Spark engine to run complex large-scale workloads. Gluten delivers exceptional performance when run on large hardware.

You can use the following methods to provision Gluten Accelerated Spark engine:

* Provisioning through Console
* Provisioning through API

### Prerequisites
{: #prov_cpp_preq}


- You must have a subscription of {{site.data.keyword.lakehouse_short}} on Cloud.
- `<engine-home-bucket>` : You must create a storage in {{site.data.keyword.lakehouse_short}}, that will be associated with your Gluten Accelerated Spark engine to store the logs.


### Provisioning through Console
{: #prov_cpp_1}

To add a Gluten accelerated Spark engine, complete the following steps.

1. Log in to {{site.data.keyword.lakehouse_short}} console.

2. From the navigation menu, select **Infrastructure manager**.

3. To add a Gluten accelerated Spark engine, click **Add component**, Click **IBM Spark** and click **Next**.

5. In the **Add component-IBM Spark** page, from the **Type** section, select **Gluten accelerated Spark engine**.

6. In the **Add component - IBM Spark** page, configure the following details:

      a. In the **Add component - Gluten accelerated Spark engine** window, enter the **Display name** for your Gluten accelerated Spark engine.
      c. Configure the following details:

      | Field | Description |
      | --- | --- |
      | Default Spark version | Select the Spark runtime version that must be considered for processing the applications. Gluten accelerated Spark engine support version 3.4. |
      | Engine home bucket | Select the registered Cloud Object Storage bucket from the list to store the Spark events and logs that are generated while running spark applications. \n [Note]{: tag-purple} Make sure you do not select the IBM-managed bucket as Spark engine home. If you select an IBM-managed bucket, you cannot access it to view the logs. \n For more information, see [Before you begin]({{site.data.keyword.ref-prov_nspark-link}}#prereq_nspark_prov).|
      |Reserve capacity| 1. Select the **Node Type**. \n 2. Enter the number of nodes in the **No of nodes** field.     |
      |Associated catalogs (optional)| Select the catalogs that must be associated with the engine.   |
      {: caption="Provisioning Gluten accelerated Spark engine" caption-side="bottom"}

6. Click **Create**. The engine is provisioned and is displayed in the **Infrastructure Manager** page.


### Provisioning through API
{: #prov_cpp_2}

1. Use the following CURL command to create a Gluten Accelerated Spark engine.


#### V2 API


   ```bash
   curl -X POST https://`<region>`.lakehouse.cloud.ibm.com/lakehouse/api/v2/spark_engines   -H "content-type: application/json" -H "accept: application/json" -H "AuthInstanceId: `<CRN>`" -d {

       "description": "",

       "engine_details": {

           "default_version": "3.4",

           "scale_config": {

               "node_type": "small",

               "number_of_nodes": 1

           },

           "engine_home_bucket_name": "`<engine-home-bucket>`"

       },

       "engine_display_name": "`<gluten_engine_name>`",

       "associated_catalogs": [

           "<catalog_name>"

       ],

       "origin": "native",
       "type": "gluten"

   }

      }
   ```
   {: codeblock}

   Parameter values:

   * `<region>`: The region where the {{site.data.keyword.lakehouse_short}} instance is available.
   * `<CRN>`: The {{site.data.keyword.lakehouse_short}} instance CRN. You can retrieve the CRN from the {{site.data.keyword.lakehouse_short}} information page.
   * `<engine-home-bucket>` : The storage that enables you to monitor and debug the Spark application.
   * `<gluten_engine_name>`: Specify a name for the Gluten accelerated Spark engine.
   * `<catalog_name>`: Specify a name for the catalog you use. Gluten accelerated Spark supports Iceberg, Hudi, Delta, and Hive catalogs.

#### V3 API


   ```bash

   curl -X POST -H "content-type: application/json" -H "accept: application/json" -H "AuthInstanceId: {instance_id}" -d '{ "description": "spark engine description", "configuration": { "api_key": "apikey", "connection_string": "1.2.3.4", "instance_id": "spark-id", "managed_by": "fully/self" }, "display_name": "sampleEngine", "origin": "discover/external", "tags": [ "tag1", "tag2" ], "type": "spark" }' "https://{region}.lakehouse.cloud.ibm.com/lakehouse/api/v3/spark_engines"

   ```
   {: codeblock}


