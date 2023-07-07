---

copyright:
  years: 2017, 2023
lastupdated: "2023-07-07"

keywords: watsonx.data, spark, analytics, configuring
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Retrieving Hive metastore(HMS) credentials
{: #hms}

Complete the following steps to generate HMS credentials. HMS credential includes:

* API key. Follow the [steps](#hms_api) to generate the key.
* HMS endpoint (thrift url). Follow the [steps](#hms_url) to generate the thrift url.
* HMS username is by default **ibmlhapikey**

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

## Getting the HMS endpoint
{: #hms_url}

1. Log in to {{site.data.keyword.lakehouse_short}} console.
1. From the navigation menu, select **Infrastructure manager**.
1. Select the **catalog**.
1. Click **Details** to view the **catalog details** page.
1. Copy the **Metastore host**. This is your HMS endpoint (thrift url).
