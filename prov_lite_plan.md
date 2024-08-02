---

copyright:
  years: 2022, 2024
lastupdated: "2024-08-02"

keywords: watsonx.data, lite, plan, instance

subcollection: watsonxdata

---


{{site.data.keyword.attribute-definition-list}}


{:step: data-tutorial-type="step"}
{:shortdesc: .shortdesc}


# {{site.data.keyword.lakehouse_short}} Lite plan
{: #tutorial_prov_lite_1}


The **Lite** plan allows you to provision a {{site.data.keyword.lakehouse_full}} instance that is free to use, with limits on capacity (2000 Resource Units), and features for a time frame of 30 days. You can use the account to explore and familiarize yourself with {{site.data.keyword.lakehouse_short}}. For more information about the features and limitations of Lite plan, see [Lite plan](watsonxdata?topic=watsonxdata-pricing-plans-1#limitations-lite){: external}.
{: shortdesc}


After provisioning the Lite plan instance, you can monitor the resource unit usage from the Billing and Usage page available in the watsonx.data console.
IBM Cloud trial account users can have only a single active lite plan instance per account. However, if you delete the existing Lite plan instance before reaching the account cap limit of 2000 RUs, you can create a new instance and consume the remaining resource units available in the account. This applies to the paid IBM Cloud account users also. In addition, they can create multiple Lite plan instances in different [resource groups](https://cloud.ibm.com/docs/account?topic=account-rgs&interface=ui). If the account has multiple Lite instances active at the same time, the resource unit consumption for the account will be the sum of resource units consumed by each individual instance.
When the usage cap is reached, any active Lite plan instances owned by the account are disabled and you cannot create any new Lite plan instances.

To access all the features and functionalities without resource or time limit, you must have an Enterprise {{site.data.keyword.lakehouse_short}} instance in the paid IBM Cloud account.
In this tutorial, you learn how to provision {{site.data.keyword.lakehouse_short}} instance (Lite plan) and explore its features.






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



## Open the web console
{: #open_console-2}
{: step}

1. Go to **Resource list** **>** **Databases**.

2. Click your {{site.data.keyword.lakehouse_short}} instance link. The service instance page opens.

3. Click **Open web console**. The {{site.data.keyword.lakehouse_short}} web console opens.

## Reference
{: #gs_ns_2}

To explore the features of {{site.data.keyword.lakehouse_short}} web console, see [Lite plan](watsonxdata?topic=watsonxdata-tutorial_hp_intro).
