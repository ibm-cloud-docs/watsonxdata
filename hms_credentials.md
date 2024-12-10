---

copyright:
  years: 2022, 2024
lastupdated: "2024-12-10"

keywords: watsonx.data, spark, analytics, configuring
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Retrieving Metadata Service (MDS) endpoints and credentials
{: #hms}

{{site.data.keyword.lakehouse_full}} integrates with multiple entities like Spark, Db2, {{site.data.keyword.netezza_short}}, and the like. You require {{site.data.keyword.lakehouse_short}} MDS credentials to establish connection with the entities at the time of integration.
{: shortdesc}

You must generate the following MDS credentials.


* MDS endpoint (thrift url). Follow the [steps](#hms_url) to generate the thrift url.
* MDS username is by default **ibmlhapikey**
* Certificate verification. Follow the [steps](#hms_cert) to verify the certificate.
* API key. Follow the [steps](#hms_api) to generate the key.


## Prerequisites
{: #hms-preq}

{{site.data.keyword.lakehouse_full}} uses the 4.0.0-alpha-2 version of MDS and you must have the support thrift protocol jar to ensure compatibility.


## Getting the MDS endpoint
{: #hms_url}

1. Log in to {{site.data.keyword.lakehouse_short}} console.
1. From the navigation menu, select **Infrastructure manager**.
1. Select the **catalog**.
1. Click **Details** to view the **catalog details** page.
1. Copy the **Metastore Thrift endpoint**. This is your MDS endpoint (thrift url).

   For Unity and Iceberg Catalog REST API, copy **Metastore REST endpoint**.
   {: note}

## Generating API key
{: #hms_api}

1. In the IBM Cloud console, go to **Manage** and create **service ID**. For information about creating service ID, see [Creating a service ID](https://ondeck.console.cloud.ibm.com/docs/account?topic=account-serviceids&interface=ui#create_serviceid).
1. In the **Access** tab, from **Access policies**, click **Assign access**. The **Assign access to Doc Service** page opens.
1. Select **Access policy**. In the **Create policy** section, select the **UI** tab.
1. Search and select **{{site.data.keyword.lakehouse_short}}** from the **Service** field.
1. Click **Next**. The **Access policies** section is reflected with the role.
1. Go to **Manage > Access (IAM)**, and select the **Service IDs**.
1. Identify the row of the service ID for which you want to select an API key. Select the name of the service ID.
1. Click **API keys**.
1. Click **Create**.
1. Specify a name and description to easily identify the API key.
1. Click **Create**.
1. Save your API key by copying or downloading it to secure location.
