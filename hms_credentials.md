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

{{site.data.keyword.lakehouse_full}} integrates with multiple entities like Spark, Db2, {{site.data.keyword.netezza_short}}, and the like. You require {{site.data.keyword.lakehouse_short}} MDS credentials and enpoint to establish connection with the entities at the time of integration.
{: shortdesc}

MDS username is by default **ibmlhapikey**.

## Generating API key
{: #hms_api}

1. As the {{site.data.keyword.lakehouse_short}} administrator, you can:

   1. [Create service IDs](https://ondeck.console.cloud.ibm.com/docs/account?topic=account-serviceids&interface=ui#create_serviceid)
   2. [Invite users and grant permissions](https://cloud.ibm.com/docs/account?topic=account-access-getstarted#group_access)

   Permission required for {{site.data.keyword.lakehouse_short}} are `MetastoreAdmin` in **Service access** and appropriate roles in **Platform access**.
   {: note}
1. Generate an API key. for more information, see:

   - [Creating an API key for users or user groups](https://cloud.ibm.com/docs/account?topic=account-userapikey&interface=ui#create_user_key)
   - [Creating an API key for a service ID](https://cloud.ibm.com/docs/account?topic=account-serviceidapikeys&interface=ui#create_service_key)

## Getting the MDS endpoint
{: #hms_url}

1. Log in to {{site.data.keyword.lakehouse_short}} console.
1. From the navigation menu, select **Infrastructure manager**.
1. Select the **catalog**.
1. Click **Details** to view the **catalog details** page.
1. Copy the endpoint:

   1. **Metastore Thrift endpoint**: This is your Hive interface endpoint for thrift.
   1. **Metastore REST endpoint**: Use this for Unity and Iceberg Catalog REST API.

   You can retrive the endpoints using API. For more information, see [Get catalog API](https://cloud.ibm.com/apidocs/watsonxdata#get-catalog).
