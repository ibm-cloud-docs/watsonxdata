---

copyright:
  years: 2022, 2024
lastupdated: "2024-11-29"

keywords: watsonx.data, spark, analytics, configuring
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Configuring {{site.data.keyword.iae_short}}
{: #lh-config-ae}

You can configure {{site.data.keyword.iae_full_notm}} instance to connect to the {{site.data.keyword.lakehouse_full}} instance by setting {{site.data.keyword.lakehouse_short}} configurations and Spark related configuration as the default configuration for the {{site.data.keyword.iae_full_notm}} instance.
{: shortdesc}

You can configure {{site.data.keyword.iae_short}} instance with default settings in one of the following ways:

* [Configure by using the {{site.data.keyword.Bluemix_short}} console](#lh-cons-config-ae).
* [Configure by using the {{site.data.keyword.iae_short}} API](#lh-api-config-ae).
* [Configure by using the {{site.data.keyword.iae_short}} CLI](#lh-cli-config-ae).


## Prerequisites
{: #lh-preq-ae}

Ensure you have the following instances ready:

* {{site.data.keyword.lakehouse_full}} instance.
* {{site.data.keyword.iae_full_notm}} instance.

Fetch the following information from IBM® watsonx.data:
* MDS URL from {{site.data.keyword.lakehouse_short}}.For more information on getting the MDS credentials, see [Getting Metadata Service (MDS) Credentials]({{site.data.keyword.ref-hms-link}}){: external}.
* MDS Credentials from {{site.data.keyword.lakehouse_short}}. For more information on getting the MDS credentials, see [Getting Metadata Service (MDS) Credentials]({{site.data.keyword.ref-hms-link}}){: external}.

## Configuring {{site.data.keyword.iae_short}} instance by using {{site.data.keyword.Bluemix_short}} console
{: #lh-cons-config-ae}

To configure your {{site.data.keyword.iae_short}} instance from the {{site.data.keyword.Bluemix_short}} Resource list, complete the following steps:


1. Log in to your {{site.data.keyword.Bluemix_short}} account.
1. Access the [{{site.data.keyword.Bluemix_short}} Resource list](https://cloud.ibm.com/resources).
1. Search your {{site.data.keyword.iae_short}} instance and click the instance to see the details.
1. Click **Manage > Configuration** to view the configuration.
1. In the **Default Spark configuration** section, click **Edit**.
1. Add the following configuration to the **Default Spark configuration** section.

    ```bash
    spark.sql.catalogImplementation = hive
    spark.sql.extensions = org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions
    spark.sql.iceberg.vectorization.enabled = false
    spark.sql.catalog.lakehouse = org.apache.iceberg.spark.SparkCatalog
    spark.sql.catalog.lakehouse.type = hive
    spark.sql.catalog.lakehouse.uri = <mds-thrift-endpoint-from-watsonx.data> for example (thrift://81823aaf-8a88-4bee-a0a1-6e76a42dc833.cfjag3sf0s5o87astjo0.databases.appdomain.cloud:32683)
    spark.hive.metastore.client.auth.mode = PLAIN
    spark.hive.metastore.client.plain.username = <mds-user-from-watsonx.data> (for example, ibmlhapikey)
    spark.hive.metastore.client.plain.password = <mds-password-from-watsonx.data>
    spark.hive.metastore.use.SSL = true
    spark.hive.metastore.truststore.type = JKS
    spark.hive.metastore.truststore.path = file:///opt/ibm/jdk/lib/security/cacerts
    spark.hive.metastore.truststore.password = changeit
    ```
    {: codeblock}

Parameter value:
* mds-thrift-endpoint-from-watsonx.Data: Specify the credentials for watsonx.data.
* mds-user-from-watsonx.Data: The watsonx.data username.
* mds-password-from-watsonx.Data: The watsonx.data password.

## Configuring {{site.data.keyword.iae_short}} instance by using {{site.data.keyword.iae_short}} API
{: #lh-api-config-ae}

To configure your {{site.data.keyword.iae_full_notm}} instance from the {{site.data.keyword.iae_short}} API, complete the following steps:
{: shortdesc}

1. Generate an IAM token to connect to the {{site.data.keyword.iae_full_notm}} API. For more information about how to generate an IAM token, see [IAM token](https://cloud.ibm.com/docs/AnalyticsEngine?topic=AnalyticsEngine-retrieve-endpoints-serverless#endpoints-cli).

1. Run the following API command to invoke the {{site.data.keyword.iae_short}} API by using the generated IAM token.

```bash
curl -X PATCH --location --header "Authorization: Bearer {IAM_TOKEN}" --header "Accept: application/json" --header "Content-Type: application/merge-patch+json" --data '{
<CONFIGURATION_DETAILS>
}' "{BASE_URL}/v3/analytics_engines/{INSTANCE_ID/default_configs"
```
{: codeblock}

Parameter value:
* IAM_TOKEN: Specify the API token generated for the {{site.data.keyword.iae_short}} API.
* CONFIGURATION_DETAILS: Copy and paste the following command:
    ```bash
    {
    "spark.sql.catalogImplementation": "hive",
    "spark.sql.extensions": "org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions",
    "spark.sql.iceberg.vectorization.enabled": "false",
    "spark.sql.catalog.lakehouse": "org.apache.iceberg.spark.SparkCatalog",
    "spark.sql.catalog.lakehouse.type": "hive",
    "spark.sql.catalog.lakehouse.uri": "<mds-thrift-endpoint-from-watsonx.data> for example (thrift://81823aaf-8a88-4bee-a0a1-6e76a42dc833.cfjag3sf0s5o87astjo0.databases.appdomain.cloud:32683) ",
    "spark.hive.metastore.client.auth.mode": "PLAIN",
    "spark.hive.metastore.client.plain.username": "<mds-user-from-watsonx.data> (for example, ibmlhapikey)",
    "spark.hive.metastore.client.plain.password": "<mds-password-from-watsonx.data>",
    "spark.hive.metastore.use.SSL": "true",
    "spark.hive.metastore.truststore.type": "JKS",
    "spark.hive.metastore.truststore.path": "file:///opt/ibm/jdk/lib/security/cacerts",
    "spark.hive.metastore.truststore.password": "changeit"
    }
    ```
    {: codeblock}

* BASE_URL: The {{site.data.keyword.iae_short}} URL for the region where you provisioned the instance. For example, api.region.ae.ibmcloud.com.
* INSTANCE_ID: The {{site.data.keyword.iae_short}} instance ID. For more information about how to retrieve an instance ID, see [Obtaining the service endpoints](https://cloud.ibm.com/docs/AnalyticsEngine?topic=AnalyticsEngine-retrieve-endpoints-serverless#endpoints-cli).
* mds-thrift-endpoint-from-watsonx.data: Specify the credentials for {{site.data.keyword.lakehouse_short}}.
* mds-user-from-watsonx.data: The {{site.data.keyword.lakehouse_short}} username.
* mds-password-from-watsonx.data: The {{site.data.keyword.lakehouse_short}} password.

## Configuring {{site.data.keyword.iae_short}} instance by using {{site.data.keyword.iae_short}} CLI
{: #lh-cli-config-ae}

To specify the configuration settings for your {{site.data.keyword.iae_full_notm}} instance from CLI, complete the following steps:


Run the following command :

```bash
ibmcloud analytics-engine-v3 instance default-configs-update [--id INSTANCE_ID] --body BODY
```
{: codeblock}

Parameter value:
* BODY: Copy and paste the following configuration information:
    ```bash
    {
    "spark.sql.catalogImplementation": "hive",
    "spark.sql.extensions": "org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions",
    "spark.sql.iceberg.vectorization.enabled": "false",
    "spark.sql.catalog.lakehouse": "org.apache.iceberg.spark.SparkCatalog",
    "spark.sql.catalog.lakehouse.type": "hive",
    "spark.sql.catalog.lakehouse.uri": "<mds-thrift-endpoint-from-watsonx.data> for example (thrift://81823aaf-8a88-4bee-a0a1-6e76a42dc833.cfjag3sf0s5o87astjo0.databases.appdomain.cloud:32683) ",
    "spark.hive.metastore.client.auth.mode": "PLAIN",
    "spark.hive.metastore.client.plain.username": "<mds-user-from-watsonx.data> (for example, ibmlhapikey)",
    "spark.hive.metastore.client.plain.password": "<mds-password-from-watsonx.data>",
    "spark.hive.metastore.use.SSL": "true",
    "spark.hive.metastore.truststore.type": "JKS",
    "spark.hive.metastore.truststore.path": "file:///opt/ibm/jdk/lib/security/cacerts",
    "spark.hive.metastore.truststore.password": "changeit"
    }
    ```
    {: codeblock}

* INSTANCE_ID: The {{site.data.keyword.iae_short}} instance ID. For more information about how to retrieve an instance ID, see [Obtaining the service endpoints](https://cloud.ibm.com/docs/AnalyticsEngine?topic=AnalyticsEngine-retrieve-endpoints-serverless#endpoints-cli)
* mds-thrift-endpoint-from-watsonx.data: Specify the credentials for {{site.data.keyword.lakehouse_short}}. For more information on getting the MDS credentials, see [Getting Metadata Service (MDS) Credentials]({{site.data.keyword.ref-hms-link}}).
* mds-user-from-watsonx.data: The {{site.data.keyword.lakehouse_short}} username. For more information on getting the MDS credentials, see [Getting Metadata Service (MDS) Credentials]({{site.data.keyword.ref-hms-link}}){: external}.
* mds-password-from-watsonx.data: The {{site.data.keyword.lakehouse_short}} password. For more information on getting the MDS credentials, see [Getting Metadata Service (MDS) Credentials]({{site.data.keyword.ref-hms-link}}){: external}.

To view logs of Spark application ran on {{site.data.keyword.iae_full_notm}} you have to enable logging. For more information, see [Configuring and viewing logs](https://cloud.ibm.com/docs/AnalyticsEngine?topic=AnalyticsEngine-viewing-logs){: external}.
{: note}
