---

copyright:
  years: 2022, 2024
lastupdated: "2024-10-15"

keywords: lakehouse, watsonx data, provision, endpoint, resource
subcollection: watsonxdata


---


{{site.data.keyword.attribute-definition-list}}

# Choosing {{site.data.keyword.lakehouse_short}} plan and provisioning an instance
{: #getting-started}

{{site.data.keyword.lakehouse_full}} is a data management solution for collecting, storing, querying, and analyzing all your enterprise data with a single unified data platform. It provides a flexible and reliable platform that is optimized to work on open data formats.
{: shortdesc}

{{site.data.keyword.lakehouse_short}} can be deployed in one of the following ways:
- Stand-alone software on Red Hat OpenShift. For more information, see [{{site.data.keyword.lakehouse_full}}](https://www.ibm.com/docs/en/watsonxdata/1.1.x).
- On Cloud Pak for Data. For more information, see [{{site.data.keyword.lakehouse_full}} on Cloud Pak for Data](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.8.x?topic=services-watsonxdata).
- SaaS - on IBM Cloud and AWS.
- Additionally the watsonx.data Developer edition can be installed for POC purposes. For more information, see [{{site.data.keyword.lakehouse_full}}](https://www.ibm.com/docs/en/watsonxdata/1.1.x).


## Before you begin
{: #prereqs}

You need to have an [{{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/registration){: external}.

The access to provision IBM Cloud resources is governed by using [IAM access](https://cloud.ibm.com/docs/account?topic=account-userroles&interface=ui) and [account management services](https://cloud.ibm.com/docs/account?topic=account-account-services&interface=ui). You must have **Administrator** privileges to access the resource group in which you need to create the resources.
{: note}


## Review resource unit consumption
{: #hp_view_lit}

To understand about the resource unit consumption for the components in the {{site.data.keyword.lakehouse_short}} instance, follow the steps:

1. Go to the [{{site.data.keyword.cloud_notm}} catalog](https://cloud.ibm.com/catalog) page, find the **{{site.data.keyword.lakehouse_short}}** tile and click it. The [{{site.data.keyword.lakehouse_short}} provisioning](https://cloud.ibm.com/watsonxdata) page opens.

1. Select the **About** tab.

1. You can read through the **Summary** and **Features**.

1. In the **Pricing estimator**, provide the following inputs and review the **Estimate summary** to assess the hourly cost for the resource units.


   | Field | Description |
   |--------------------------|----------------|
   |Select platform |Select the platform.|
   |License |Select the plan.|
   |Support services|Includes the necessary access control and metastore. The resource unit quantity is visible on the right.|
   |Engine/Service 1|Select the engine or service of your choice.|
   |If you select **Presto**|**a**. Select the coordinated node type and number of coordinated nodes. The resource unit quantity is visible on the right. \n **b**. Select the worker node type and number of worker nodes. The resource unit quantity is visible on the right.|
   |If you select **Milvus**|Select the size of your choice. The resource unit quantity is visible on the right.|
   |If you select **Spark**|Select the size of your choice. The resource unit quantity is visible on the right.|
   {: caption="Pricing estimator" caption-side="bottom"}

## Provision an instance
{: #create}

To provision an instance, choose one of the following:

* [Lite plan](watsonxdata?topic=watsonxdata-tutorial_prov_lite_1)
* [Enterprise plan](watsonxdata?topic=watsonxdata-getting-started_1)
