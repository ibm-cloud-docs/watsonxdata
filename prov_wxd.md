---

copyright:
  years: 2022, 2024
lastupdated: "2024-10-16"

keywords: lakehouse, watsonx data, provision, endpoint, resource
subcollection: watsonxdata


---


{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.lakehouse_full}} subscription plans
{: #getting-started}

{{site.data.keyword.lakehouse_full}} is a data management solution for collecting, storing, querying, and analyzing all your enterprise data with a single unified data platform. It provides a flexible and reliable platform that is optimized to work on open data formats.
{: shortdesc}

{{site.data.keyword.lakehouse_short}} can be deployed in one of the following ways:
- Stand-alone software on Red Hat OpenShift. For more information, see [{{site.data.keyword.lakehouse_full}}](https://www.ibm.com/docs/en/watsonxdata/1.1.x).
- On IBM Software Hub. For more information, see [{{site.data.keyword.lakehouse_full}} on IBM Software Hub](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.8.x?topic=services-watsonxdata).
- SaaS - on IBM Cloud and AWS. For more information, see [IBM watsonx.data as a Service on AWS](https://www.ibm.com/docs/en/watsonx/watsonxdata/aws).
- Additionally the watsonx.data Developer edition can be installed for POC purposes. For more information, see [{{site.data.keyword.lakehouse_full}}](https://www.ibm.com/docs/en/watsonxdata/1.1.x).


The SaaS deployment of watsonx.data is offered under two pricing plans, as follows:

* [Lite plan](#lite-plan-1) - Give link to https://test.cloud.ibm.com/docs-draft/watsonxdata?topic=watsonxdata-tutorial_prov_lite_1

* [Enterprise plan](#enterprise-plan) - Give link to https://test.cloud.ibm.com/docs-draft/watsonxdata?topic=watsonxdata-getting-started_1

Each region has a finite number of {{site.data.keyword.lakehouse_short}} instances that are provisioned based on the current compute capacity. Regions might reach their capacity limits temporarily. While IBM adds additional capacity, you can either wait or redirect your request to another region. If the resource capacity is exceeded, you get the following message.

```text
The new instance cannot be created because of resource capacity restrictions. Please use another region, or retry later when additional capacity may be available in the current region.
```
{: screen}

## Lite plan
{: #lite-plan-1}

The Lite plan is provided for you to try the basic features of {{site.data.keyword.lakehouse_short}} and is available to all {{site.data.keyword.Bluemix_notm}} account types like trial, pay-as-you-go, and subscription. It supports the basic features only. It is not available on AWS and is limited to one {{site.data.keyword.lakehouse_short}} instance per {{site.data.keyword.Bluemix_notm}} account (cross-regional).

### Key supported features
{: #supported-features-lite}

- Ability to monitor Resource Unit usage across Lite plan instances per an account and provision a new Lite plan instance based on the Resource Unit availability.
- Ability to pause and resume Presto engine.
- Ability to provision, unprovision, pause and resume Spark engine.
- Ability to connect to an {{site.data.keyword.Bluemix_notm}}-provided Cloud Object Storage (COS) bucket and provide credentials to your own COS or S3 bucket.
- Ability to delete Presto, Spark, Milvus, and connections to your own bucket.

### Limitations
{: #limitations-lite}

- The Lite plan is limited to 2000 resource units (RUs) before the instance is suspended. The cap value is displayed on the [{{site.data.keyword.Bluemix_notm}} catalog provisioning][def] page and is reflected on your billing page within your {{site.data.keyword.lakehouse_short}} instance upon provisioning. Your plan expires on reaching either the cap limit of 2000 RUs or exceeding the trial period of 30 days.
- The Lite plan is limited to a maximum of one Presto engine, one Spark engine (small size, single node) or Milvus service with starter size (1.25 RUs per hour) or all three.
- The Lite plan is limited to the smallest node sizes and profiles for each engine and service. You cannot increase the node size.
- The Lite plan instances cannot be used for production purposes.
- The Lite plan might be removed anytime.
- The Lite instances are unrecoverable (no BCDR).
- Engine scaling functionality is not available in the Lite plan.
- Milvus back up is not available with the Lite plan.

You must be connected to your own bucket to save and backup any data that is external to the Lite instance before full consumption of the Lite plan resource units.
{: important}

To upgrade to another plan, you must have a pay-as-you-go or subscription {{site.data.keyword.Bluemix_notm}} account and provision a distinct Enterprise instance of {{site.data.keyword.lakehouse_short}}.
{: note}

## Enterprise plan
{: #enterprise-plan}

You must have a pay-as-you-go or subscription {{site.data.keyword.Bluemix_notm}} account to avail the Enterprise plan. It is available on {{site.data.keyword.Bluemix_notm}} and AWS environments. Presto engine and Milvus service are available with this plan.

### Key supported features
{: #supported-features-ep}

- Ability to scale (increase and decrease) node sizes for Presto engines.
- Ability pause and resume Presto engines.





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
