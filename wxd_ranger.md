---

copyright:
  years: 2022, 2024
lastupdated: "2024-10-10"

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


## Procedure
{: #ranger_3}

1. Complete the following steps to create a service in the Ranger.

    a. Log in to Apache Ranger by using the username and password.

    b. The home page lists all the services that are already configured under different resources. To create a new service, click the + icon next to the PRESTO resource.

    c. Provide the following details:

     | Field | Description |
     |--------------------------|----------------|
     |  Username |	admin|
     |  Password	| UXXXXXXR|
     |jdbc.url |	Provide the JDBC URL.|
     {: caption="Apache Ranger policy " caption-side="bottom"}


    d. The service is successfully added in the PRESTO resource list. Click the service name to verify that the default policies are added.

    The testing might fail initially, you can re-test the connection after saving the details since the default policies will be automatically added after saving.
    {: note}

2. Complete the following steps to enable and configure Apache Ranger in watsonx.data.

    a. Log in to watsonx.data console.

    b. From the navigation menu, select Access control.

    c. Click the **Integrations** tab.

    d. Click **Integrate service**. The Integrate service window opens.

    e. In the **Integrate service** window, provide the following details:

     | Field | Description |
     |--------------------------|----------------|
     |Service	|Select Apache Ranger.|
     |URL	|The URL of Apache Ranger.|
     |Username|	The admin credentials.|
     |Password	|The admin credentials.|
     |List resources|	Click the link to load the resources that are available in the Apache Ranger server.|
     |Resources	|Select the resource for which the Apache Ranger policy must be enabled.|
     |Enable data policy within watsonx.data	|Select the checkbox to enable data policy along with Apache Ranger policy.|
     {: caption="Integrate service " caption-side="bottom"}


    f. Click **Integrate**. The Apache Ranger policy is integrated and listed in the Access Control page.

3. Complete the following steps to verify access control :

    a. Log in to watsonx.data instance.

    b. From the navigation menu, click **Query workspace**.

    c. Execute a simple query. The access denied error appears as currently no policies are defined in the Ranger for the user.

4. Complete the following steps to grant permissions to the user:

    a. Log in to **Apache Ranger**.

    b. Grant the required permission to the test user.

    c. Scroll down to the bottom, click the **Save** button.

    d. Log in to watsonx.data instance and execute a query again. The access is allowed for the user after adding policies in the Ranger.

## Limitations
{: #ranger_4}

* In Apache Iceberg catalog, an error occurs if a policy is not defined for the snapshots views related to the tables in Ranger. You must manually define policies in Apache Ranger to eliminate the error.
* watsonx.data supports only access control feature for Apache Ranger integration in 2.0.0 release.
