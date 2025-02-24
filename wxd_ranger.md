---

copyright:
  years: 2022, 2025
lastupdated: "2025-02-24"

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

# Enabling Apache Ranger policy for resources
{: #ranger_1}

IBM watsonx.data now supports Apache Ranger policies to allow comprehensive data security on integrating with multiple governance tools and engines.
{: shortdesc}


## Before you begin
{: #ranger_2}

Ensure you have the following details:

* IBM watsonx.data instance.
* Apache Ranger is provisioned.
* The Presto (Java) JDBC URL and credentials in watsonx.data.
* Administrator must add users and groups manually.
* You can only integrate with one of the following policy engines starting with watsonx.data version 2.1.
   * Apache Ranger
   * IBM Knowledge Catalog


## Creating policies for Presto and Spark in Ranger
{: #ranger_3}

IBM watsonx.data uses the policies defined under the following service types in Ranger to allow data security on catalogs(Iceberg, Hive and Hudi), buckets, schemas and tables.
* Presto : Create resource policies in this Ranger service type to enforce security on catalogs(Iceberg, Hive and Hudi), buckets, schemas and tables used by Presto engine in watsonx.data.
* and Hadoop SQL : Create resource policies in this Ranger service type to enforce security on catalogs(Iceberg, Hive and Hudi), buckets, schemas and tables used by Spark engine in watsonx.data.


Complete the following steps to create a service in the Ranger.

1. Log in to Apache Ranger by using the username and password.
1. The **Service Manager** page lists all the resources and available services under them. For more information about the different resources, see [Service Manager](https://cwiki.apache.org/confluence/display/RANGER/Apache+Ranger+0.5+-+User+Guide#ApacheRanger0.5UserGuide-ServiceManager(AccessManager)).
1. Click **Resource** tab and select one of the following resources depending on your use case.
   * PRESTO : Create policies for Presto engine in watsonx.data.
   * Hadoop SQL : Create policies for Spark engine in watsonx.data.
1. Click the **Add New Service** (+) icon against the required service type and create a new service to define policies. For more information about the different resources, see [Service Manager](https://cwiki.apache.org/confluence/display/RANGER/Apache+Ranger+0.5+-+User+Guide#ApacheRanger0.5UserGuide-ServiceManager(AccessManager)).


You can also select an existing service to define policies. To define Ranger policies for Presto, you must create a service under PRESTO section and to define Ranger policies for Spark, you must create a service under Hadoop SQL section.
{: note}

1. Create policy against the new (or existing) service. To do that, see [Policy Manager](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=57901344#RangerUserGuide(workinprogress)-PolicyManager).

The service is successfully added in the respective resource list. Click the service name to verify that the default policies are added.


## Associating Ranger policies for Presto and Spark in watsonx.data
{: #ranger_10}

Complete the following steps to enable and configure Apache Ranger in watsonx.data.

1. Log in to watsonx.data console.
1. From the navigation menu, select **Access control**.
1. Click the **Integrations** tab.
1. Click **Integrate service**. The Integrate service window opens.
1. In the **Integrate service** window, provide the following details:

   | Field | Description |
   |--------------------------|----------------|
   |Service	|Select Apache Ranger.|
   |URL	|The URL of Apache Ranger.|
   |Username|	The admin credentials.|
   |Password	|The admin credentials.|
   |List resources|	Click the link to load the resources that are available in the Apache Ranger server.|
   |Resources	|Select the resource for which the Apache Ranger policy must be enabled.|
   |Policy Cache Time Configuration| The time taken to refresh the newly defined Ranger policies.|
   |Enable data policy within watsonx.data	|Select the checkbox to enable data policy along with Apache Ranger policy.|
   {: caption="Integrate service " caption-side="bottom"}


1. Click **Integrate**. The Apache Ranger policy is integrated and listed in the **Access Control** page.

## Verify the integration
{: #ranger_11}


Complete the following steps to verify access control :

1. Log in to watsonx.data instance.
1. From the navigation menu, click **Query workspace**.
1. Execute a simple query. The access denied error appears as currently no policies are defined in the Ranger for the user.


## Granting permission to users
{: #ranger_12}


Complete the following steps to grant permissions to the user:

1. Log in to **Apache Ranger**.

1. Grant the required permission to the test user.

1. Scroll down to the bottom, click the **Save** button.

1. Log in to watsonx.data instance and execute a query again. The access is allowed for the user after adding policies in the Ranger.

## Limitations
{: #ranger_4}

* In Apache Iceberg catalog, an error occurs if a policy is not defined for the snapshots views related to the tables in Ranger. You must manually define policies in Apache Ranger to eliminate the error.
* watsonx.data supports only access control feature for Apache Ranger integration in 2.0.0 release.
