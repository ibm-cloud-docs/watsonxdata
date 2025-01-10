---

copyright:
  years: 2022, 2024
lastupdated: "2024-12-25"

keywords: lakehouse, engine, watsonx.data
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

# Provisioning a Spark engine
{: #spl_engine}

{{site.data.keyword.lakehouse_full}} allows you to add Spark engines. You can either provision a native Spark engine or register an external Spark engine. Native Spark engine is a compute engine that resides within IBM® watsonx.data. External Spark engines are engines that exist in a different environment from where watsonx.data is available.
{: shortdesc}

Support for Spark 3.3 runtime is deprecated and the default version will be changed to Spark 3.4 runtime. To ensure a seamless experience and to leverage the latest features and improvements, switch to Spark 3.4.
{: important}

To add a Spark engine, complete the following steps.

1. Log in to {{site.data.keyword.lakehouse_short}} console.

2. From the navigation menu, select **Infrastructure manager**.

3. To add a Spark engine, click **Add component** and click **Next**.

5. In the **Add component** page, from the **Engines** section, select **IBM Spark**.

6. In the **Add component - IBM Spark** page, configure the following details:

      a. In the **Add component - IBM Spark** window, enter the **Display name** for your Spark engine.

      b. Choose the **Registration mode**. Based on your requirement, you can select one of the following options:

      - **Create a native Spark engine** : To provision a native Spark engine.
      - **Register an external Spark engine** : To register an external Spark engine.


      c. If you choose **Create a native Spark engine**, configure the following details:

      | Field | Description |
      | --- | --- |
      | Default Spark version | Select the Spark runtime version that must be considered for processing the applications. |
      | Engine home bucket | Select the registered Cloud Object Storage bucket from the list to store the Spark events and logs that are generated while running spark applications. \n [Note]{: tag-purple} Make sure you do not select the IBM-managed bucket as Spark Engine home. If you select an IBM-managed bucket, you cannot access it to view the logs. \n For more information, see [Before you begin]({{site.data.keyword.ref-prov_nspark-link}}#prereq_nspark_prov).|
      |Reserve capacity| 1. Select the **Node Type**. \n 2. Enter the number of nodes in the **No of nodes** field.     |
      |Associated catalogs (optional)| Select the catalogs that must be associated with the engine.   |
      {: caption="Provisioning Spark engine" caption-side="bottom"}

      [Note]{: tag-purple} Provisioning time of the native Spark engine varies depending on the number and type of nodes that you add to the engine.


      d. If you choose **Register an external Spark engine**, configure the following details:


      | Field      | Description    |
      |--------------------------------|--------------------------------------------------------------------------------------------|
      | Display name   | Enter your compute engine name.  |
      | Instance API endpoint | Enter the IBM Analytics engine instance endpoint. For more information, see [Retrieving service endpoints](https://cloud.ibm.com/docs/AnalyticsEngine?topic=AnalyticsEngine-retrieve-endpoints-serverless)  |
      | API key   | Enter the API key. |
      {: caption="Registering IBM Analytics Engine (Spark)" caption-side="bottom"}


6. Click **Create**. The engine is provisioned and is displayed in the **Infrastructure Manager** page.

## Related API
{: #spark_api}

For information on related API, see
* [Create Spark engine](https://cloud.ibm.com/apidocs/watsonxdata#create-spark-engine)
* [Pause engine](https://cloud.ibm.com/apidocs/watsonxdata#pause-spark-engine)
* [Resume engine](https://cloud.ibm.com/apidocs/watsonxdata#resume-spark-engine)
* [Scale Spark engine](https://cloud.ibm.com/apidocs/watsonxdata#scale-spark-engine)
* [List Spark version](https://cloud.ibm.com/apidocs/watsonxdata#list-spark-versions)
