---

copyright:
  years: 2022, 2024
lastupdated: "2024-05-31"

keywords: watsonx.data, lite, plan, instance

subcollection: watsonxdata

content-type: tutorial
account-plan: paid
completion-time: 0.25h
---


{{site.data.keyword.attribute-definition-list}}


{:step: data-tutorial-type="step"}
{:shortdesc: .shortdesc}


# {{site.data.keyword.lakehouse_short}} Enterprise with BYOL (Bring Your Own License) plan
{: #tutorial_prov_byol}
{: toc-content-type="tutorial"}
{: toc-completion-time="0.25h"}

{{site.data.keyword.lakehouse_full}} Enterprise with BYOL (Bring Your Own License) plan is a cost-saving plan for users with a {{site.data.keyword.lakehouse_short}} license other than SaaS.
{: shortdesc}

In this tutorial, learn how to provision a {{site.data.keyword.lakehouse_short}} BYOL instance.

* [Provision an instance through UI](#byol_provision)
* [Provision an instance through CLI](#byol-by-cli)

## Provisioning Enterprise with BYOL plan through UI
{: #byol_provision}

1. Go to the [{{site.data.keyword.lakehouse_short}} provisioning](https://cloud.ibm.com/watsonxdata) page.
1. To estimate the price by using the **Pricing estimator**, see [Review resource unit consumption](../watsonxdata/getting-started.md#review-resource-unit-consumption).
1. Go to the **Create** tab and select the **Enterprise** plan from the **Select a pricing plan** section.
1. Select a location from the **Choose a location** drop-down list.

   If you choose a location where the Enterprise BYOL plan is not enabled, the system returns a message: `This plan is not available with your current account type. Upgrade to a pay-as-you-go account`.
   {: attention}

1. Select **Bring your own license (BYOL)** from the **License** drop-down list.
1. Select the checkbox under the **License** drop-down list to agree to the license terms.
1. Under the **Configure your resource** section:
   1. Enter a service name in the **Service name** column. The service name can be any string. This service name is used in the web console to identify the new deployment.
   1. Select a resource group from the **Select a resource group** drop-down list.
   1. Optional: Enter the tags and access management tags in the respective columns.
1. Agree to the license agreement by selecting the checkbox and click **Create**. The system redirects you to the **Resource list** page. You can see the instance under the **Databases** list with status **Provision in progress**.
1. Wait for the status to be **Active**. Your instance is successfully provisioned.

## Provisioning Enterprise with BYOL plan through CLI
{: #byol-by-cli}


To provision through CLI, see [Provision an instance through CLI](watsonxdata?topic=watsonxdata-getting-started_1#create-by-cli).


Make sure to include the `license` parameter while specifying the parmeters in the provisioning CLI command. If `license` parameter is not provided, the value is defaulted to `Included`.
{: important}

Consider the following example to create a new formation.


Example:


```bash
    ibmcloud resource service-instance-create <instance-name> lakehouse lakehouse-enterprise us-south -g Default -p '{"datacenter": "ibm:us-south:dal", "license": "byol"}'
```
{: codeblock}

## Open the web console
{: #open_console-1}
{: step}

1. Go to **Resource list** **>** **Databases**.

2. Click your {{site.data.keyword.lakehouse_short}} instance link. The service instance page opens.

3. Click **Open web console**. The {{site.data.keyword.lakehouse_short}} web console opens.

    <!-- 1. Log in to the console with your IBMid and password. The {{site.data.keyword.lakehouse_short}} web console opens. -->

## Next steps
{: #gs_ns-1}

To quickly get started with the {{site.data.keyword.lakehouse_short}} web console by configuring the infrastructure components, see [Quick start {{site.data.keyword.lakehouse_short}} console](watsonxdata?topic=watsonxdata-quick_start).
