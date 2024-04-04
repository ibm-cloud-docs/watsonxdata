---

copyright:
  years: 2022, 2024
lastupdated: "2024-04-03"

keywords: watsonx.data, spark, analytics, configuring
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Retrieving Hive metastore(HMS) credentials
{: #hms}

{{site.data.keyword.lakehouse_full}} integrates with multiple entities like Spark, Db2, {{site.data.keyword.netezza_short}}, and the like. You require {{site.data.keyword.lakehouse_short}} HMS credentials to establish connection with the entities at the time of integration.
{: shortdesc}

You must generate the following HMS credentials.


* HMS endpoint (thrift url). Follow the [steps](#hms_url) to generate the thrift url.
* HMS username is by default **ibmlhapikey**
* Certificate verification. Follow the [steps](#hms_cert) to verify the certificate.
* API key. Follow the [steps](#hms_api) to generate the key.


## Prerequisites
{: #hms-preq}

{{site.data.keyword.lakehouse_full}} uses the 4.0.0-alpha-2 version of HMS and you must have the support thrift protocol jar to ensure compatibility.


## Getting the HMS endpoint
{: #hms_url}

1. Log in to {{site.data.keyword.lakehouse_short}} console.
1. From the navigation menu, select **Infrastructure manager**.
1. Select the **catalog**.
1. Click **Details** to view the **catalog details** page.
1. Copy the **Metastore host**. This is your HMS endpoint (thrift url).

## Loading certificates to Java truststore
{: #hms_cert}

To establish connection with {{site.data.keyword.lakehouse_short}}, you (the integrating entities) must mount the well-known certificate along with your implementation code. You can either use the trust certificate that you have or use the java certificate. Choose the well-known certificate based on your implementation code language. For example, if your code is in Java, get the corresponding well-known certificate.

To load the well-known certificate to the truststore, update your implementation code to include the well-known certificate.

1. To use your certificate, update the truststorepath variable. Specify the path of your certificate in the `truststorePath` field. In the below example, a jvm certificate is mounted. You can mount your own well known trust certificate.

```bash
String truststorePath =
System.getProperty("java.home") + File.separator +"lib"+ File.separator + "security" + File.separator + "cacerts";

MetastoreConf.setVar(clientConf, ConfVars.SSL_TRUSTSTORE_PATH, truststorePath);
```
{: codeblock}

You can now successfully establish connection with {{site.data.keyword.lakehouse_short}}.

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
