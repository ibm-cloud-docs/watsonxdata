---

copyright:
  years: 2022, 2024
lastupdated: "2024-04-30"

keywords: watsonx.data, lite, plan, instance

subcollection: watsonxdata

content-type: tutorial
account-plan: paid
completion-time: 0.25h
---


{{site.data.keyword.attribute-definition-list}}


{:step: data-tutorial-type="step"}
{:shortdesc: .shortdesc}


# {{site.data.keyword.lakehouse_short}} Lite plan
{: #tutorial_hp_intro}
{: toc-content-type="tutorial"}
{: toc-completion-time="0.25h"}

The **Lite** plan allows you to provision an {{site.data.keyword.lakehouse_full}} instance that is free to use, with limits on capacity (2000 Resource Units), and features for a time frame of 30 days. You can use the account to explore and familiarize yourself with {{site.data.keyword.lakehouse_short}}. For more information about the features and limitations of Lite plan, see [Lite plan](watsonxdata?topic=watsonxdata-pricing-plans-1#limitations-lite){: external}.
{: shortdesc}

When the allocated Resource Units or time runs out, the instance becomes inactive and you can no longer access it.
{: important}

To access all the features and functionalities without resource or time limit, you must have an [Enterprise {{site.data.keyword.lakehouse_short}} instance](watsonxdata?topic=watsonxdata-tutorial_prov_byol){: external} in a paid IBM Cloud account.

In this tutorial, you learn how to provision {{site.data.keyword.lakehouse_short}} instance (lite plan) and explore its features.


<!-- ## Lite plan features and limitations
{: #tut_lite_pln}


* Enables provisioning of a single lite plan instance per account.
* Lite plan provides a free usage limit of 2000 Resource Units (RUs)(monitored on the **Billing and usage** page of IBM Cloud) or a time frame of 30 days. Your license expires on reaching either the cap limit of 2000 Resource Units or exceeding the trial period of 30 days.

    When the lite plan license expires, the instance becomes inactive and resources are spun down. You can delete the instance from the resource group or IBM cloud resource collection removes it after a period of 40 days.
    {: note}

* With the lite plan instance, you can create one starter Presto group which consists of 1 worker and 1 coordinator (x RUs per hour), or one starter (1.25 RUs per hour) size Milvus service, or both.
* Engine scaling functionality is not available in the lite plan.
* The Quick start path is simplified in the lite plan. For more information, see [Getting started](#hp_start).
* The **Billing and usage** facilitates monitoring of resource usage. -->

<!--
## Objective
{: #tut_lite_obj}

* Provisioning {{site.data.keyword.lakehouse_short}} instance (lite plan)
* Loading data
* Querying data

![Workflow diagram](images/lite_userjourney.svg){: caption="Figure 1. User journey" caption-side="bottom"} -->

## Before you begin
{: #hp_byb}

To provision {{site.data.keyword.lakehouse_short}} Lite plan instance, you must have a trial account (or a paid account) on the IBM Cloud.
IBM Cloud trial accounts can have only one resource group. To create an IBM Cloud trial account, see [Trial account](https://cloud.ibm.com/docs/account?topic=account-accounts#trial).


## Provisioning {{site.data.keyword.lakehouse_short}} Lite plan
{: #hp_view_1}
{: step}

To provision a Lite plan instance, see [Provisioning {{site.data.keyword.lakehouse_short}} Lite plan](watsonxdata?topic=watsonxdata-tutorial_prov_lite_1).

<!-- 1. Log in to the console with your IBMid and password. The {{site.data.keyword.lakehouse_short}} web console opens. -->

## Viewing usage
{: #hp_monitor_usg_lite}
{: step}

You can monitor the Resource Units usage level.

1. For the Lite plan, in the {{site.data.keyword.lakehouse_short}} UI, **Billing** section, you can view a widget that displays the Resource Unit consumption.

1. If the allocated Resource Units or time runs out, your Lite instance will be suspended. You can still launch the IBM Cloud instance however, cannot use it. You can manually delete your IBM Cloud Lite instance by following the steps:

    1. Log in to your IBM Cloud account.
    2. Click **Resource list**. The list of resources appears.
    3. In **Resource list**, expand **Databases**.
    4. To delete an instance, click the overflow menu icon at the end of the row and click **Delete**. A delete confirmation dialog is displayed.
    5. Click **Delete**.

    For more information to manually delete an instance, see [Deleting instance](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-delete_lh).


## Getting started with {{site.data.keyword.lakehouse_short}}
{: #hp_start}
{: step}

The Lite plan usage consumption starts when you complete quickstart. The resource units (RU) are consumed even when the {{site.data.keyword.lakehouse_short}} instance is not being used. However, RU consumption reduces if you pause or delete the engine. Therefore, pause the engines and services when not in use, to maximize the IBM Cloud Lite plan availability.
{: attention}


To simplify the steps, when you log in to the {{site.data.keyword.lakehouse_short}} web console for the first time, you are directly presented with the quick start wizard **Summary** page.

1. In the **Summary** page, review the configurations before you finish setting up your data infrastructure.

    You can also navigate to the previous pages by using the **Back** button and edit the details. For more information, see [Quick start watsonx.data console](watsonxdata?topic=watsonxdata-quick_start).
    {: note}

2. Click **Finish and go**. This displays the **Infrastructure manager** page.

3. In the **Infrastructure manager** page, you can view the engine (Presto), and already provisioned bucket and catalogs. You can add single Starter sized Milvus service, additional buckets and catalogs from the **Add Components** list.

You cannot scale the existing engine or service or add a new engine (or service). To add a new engine or service, you must delete the existing engine or service.

You can add only one Presto engine and Milvus service (Milvus with size specification, Starter - 1 Million vectors, Index Parameters - 64, Segment size (1024)). To understand the restrictions, see [Lite plan features and restrictions](watsonxdata?topic=watsonxdata-pricing-plans-1).
{: important}

## Adding your storage and querying data
{: #hp_ingest}
{: step}

For more information about how to add a storage that you own and explore how the {{site.data.keyword.lakehouse_short}} service interacts with the data you bring in, see [Adding your storage and querying data](watsonxdata?topic=watsonxdata-tutorial_prov_custbckt1)

## Saving data from a lite plan to an enterprise plan
{: #post_expry}
{: step}

When the allocated Resource Units or time expires, the instance becomes inactive and you can no longer access it.

If you choose to continue using watsonx.data by creating an Enterprise {{site.data.keyword.lakehouse_short}} instance, you can save the data from your lite plan to the enterprise plan. To do that, you need an IBM Cloud Object Store (COS) bucket to connect to your lite plan instance of watsonx.data. You can then write data to that COS bucket you own. Then, create an enterprise instance of watsonx.data, connect it to the same COS bucket that you own to keep working with the same data files.


1. Create a COS bucket to store data from the Lite plan. For more information, see [Create buckets to store data](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage#gs-create-buckets).

1. Ingest data from Lite plan instance to the COS bucket. For more information, see [Adding the storage that you own and ingesting data](watsonxdata?topic=watsonxdata-tutorial_prov_custbckt1#hp_ingest1).

2. Either before or after your lite plan has concluded, create an enterprise plan instance. For more information, see [Enterprise plan](watsonxdata?topic=watsonxdata-getting-started_1).

3. Go to the **Quick start watsonx.data console** > **Configure bucket** page, specify the COS bucket details that you own (which stores data from the Lite plan). For more information, see [Quick start {{site.data.keyword.lakehouse_short}} console](watsonxdata?topic=watsonxdata-quick_start).

When the setup is complete, the watsonx.data home page (enterprise plan) opens. From the navigation menu, select **Data manager** to view the COS storage bucket with data from the lite plan.
