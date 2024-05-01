---

copyright:
  years: 2022, 2024
lastupdated: "2024-04-30"

keywords: watsonx.data, lite, plan, instance

subcollection: watsonxdata

---


{{site.data.keyword.attribute-definition-list}}


{:step: data-tutorial-type="step"}
{:shortdesc: .shortdesc}


# {{site.data.keyword.lakehouse_short}} Lite plan
{: #tutorial_prov_lite_1}


The **Lite** plan allows you to provision an {{site.data.keyword.lakehouse_full}} instance that is free to use, with limits on capacity (2000 Resource Units), and features for a time frame of 30 days. You can use the account to explore and familiarize yourself with {{site.data.keyword.lakehouse_short}}. For more information about the features and limitations of Lite plan, see [Lite plan](watsonxdata?topic=watsonxdata-pricing-plans-1#limitations-lite){: external}.
{: shortdesc}

To access all the features and functionalities without resource or time limit, you must have an Enterprise {{site.data.keyword.lakehouse_short}} instance in the paid IBM Cloud account.
In this tutorial, you learn how to provision {{site.data.keyword.lakehouse_short}} instance (Lite plan) and explore its features.


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
Trial IBM Cloud accounts can have only one resource group.


## Provisioning {{site.data.keyword.lakehouse_short}} Lite plan
{: #hp_view_1}



1. Go to the [{{site.data.keyword.lakehouse_short}} provisioning](https://cloud.ibm.com/watsonxdata) page.

1. Click the **Create** tab. Select IBM Cloud as the cloud platform to deploy {{site.data.keyword.lakehouse_short}}. In the **Management method** field, **Fully managed** is the default option, which indicates that IBM manages all the network complexities.

   Click **About** tab and read through to understand about the resource units consumed by engine/service, and estimate your consumption of 2000 RUs in the {{site.data.keyword.lakehouse_short}} Lite plan instance.
   {: note}

1. In the **Select a pricing plan** field, select **Lite**.

1. Select a location from the **Choose a location** drop-down list.

1. Enter the service name. The service name can be any string. This service name is used in the web console to identify the new deployment.

1. Select resource group. For IBM Cloud trial accounts, you cannot create additional resource groups. The default resource group is the only option available for selection.
    Trial IBM Cloud accounts can have only one resource group.
    {: note}

1. Optional: Enter the tags and access management tags.

1. In the **Summary** page, review the license agreement and select the checkbox to acknowledge the agreement.

1. Click **Create**. The message “instance is being provisioned” is displayed and the **Resource list** opens.

1. From the **Resource list** page, under the **Databases** category, you can see that the status for your instance as, **Provision in progress**. Click the {{site.data.keyword.lakehouse_short}} instance link when the status changes to **Active**.

1. Click **Open web console** and provide the Multi-Factor Authentication (MFA) details to launch the {{site.data.keyword.lakehouse_short}} Console.

<!-- 1. Log in to the console with your IBMid and password. The {{site.data.keyword.lakehouse_short}} web console opens. -->

## Open the web console
{: #open_console-2}
{: step}

1. Go to **Resource list** **>** **Databases**.

2. Click your {{site.data.keyword.lakehouse_short}} instance link. The service instance page opens.

3. Click **Open web console**. The {{site.data.keyword.lakehouse_short}} web console opens.

## Reference
{: #gs_ns_2}

To explore the features of {{site.data.keyword.lakehouse_short}} web console, see [Lite plan](watsonxdata?topic=watsonxdata-tutorial_hp_intro).
