---

copyright:
  years: 2022, 2024
lastupdated: "2024-09-24"

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


Provisioning a Lite plan instance is use case driven. Depending on the following use cases, you are presented with a Console UI that include components (engines, services and storages) that are specific to the selected use case.

* **Generative AI** : You can explore Generative AI usecases using this use case. The provisioned instance includes Presto, Milvus and Spark.
* **High Performance BI** : You can explore BI visualization functionalities using this use case. The provisioned instance includes Presto C++ and Spark only.
* **Data Engineering Workloads** : Data engineers can use the option to explore various workloads driven use cases. The provisioned instance includes Presto Java + and Spark only.


After provisioning the Lite plan instance, you can monitor the resource unit usage from the Billing and Usage page available in the watsonx.data console.
IBM Cloud trial account users can have only a single active lite plan instance per account. However, if you delete the existing Lite plan instance before reaching the account cap limit of 2000 RUs, you can create a new instance and consume the remaining resource units available in the account. This applies to the paid IBM Cloud account users also. In addition, they can create multiple Lite plan instances in different [resource groups](https://cloud.ibm.com/docs/account?topic=account-rgs&interface=ui). If the account has multiple Lite instances active at the same time, the resource unit consumption for the account will be the sum of resource units consumed by each individual instance.
When the usage cap is reached, any active Lite plan instances owned by the account are disabled and you cannot create any new Lite plan instances.

To access all the features and functionalities without resource or time limit, you must have an Enterprise {{site.data.keyword.lakehouse_short}} instance in the paid IBM Cloud account.
In this tutorial, you learn how to provision {{site.data.keyword.lakehouse_short}} instance (Lite plan) and explore its features.






## Before you begin
{: #hp_byb}

To provision {{site.data.keyword.lakehouse_short}} Lite plan instance, you must have a trial account (or a paid account) on the IBM Cloud.
Trial IBM Cloud accounts can have only one resource group.


## Provisioning {{site.data.keyword.lakehouse_short}} Lite plan through UI
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

1. You can provision the Lite plan instance based on the following use cases. Select one of the use cases from the list to proceed.

    * **Generative AI** : The provisioned instance includes Presto, Milvus and Spark.
    * **High Performance BI** : The provisioned instance includes Presto C++ and Spark only.
    * **Data Engineering Workloads** : The provisioned instance includes Presto Java + and Spark only.


1. In the **Summary** page, review the license agreement and select the checkbox to acknowledge the agreement.

1. Click **Create**. The message “instance is being provisioned” is displayed and the **Resource list** opens.





## Provisioning {{site.data.keyword.lakehouse_short}} Lite plan through CLI
{: #create-lite-cli}

1. Log in to `cloud.ibm.com`.

   ```bash
   ibmcloud login --sso -a https://cloud.ibm.com
   ```
   {: codeblock}

2. Select an account on which you want to create an instance.

3. Create a new formation.

    ```bash
    ibmcloud resource service-instance-create <instance-name> lakehouse lakehouse-lite <region> -g <resource-group> -p '{"datacenter": "<data-center>","cloud_type": "<cloud-type>","use_case": "<use_case_template>"}'
    ```
    {: codeblock}

    - `instance-name`: Name of the instance. For example, watsonx.data-abc.
    - `lakehouse`: {{site.data.keyword.lakehouse_short}} service
    - `lakehouse-lite`: Plan ID
    - `region`: The available regions are `eu-de`, `us-south`, `jp-tok`, `eu-gb`, and `au-syd`.
    - `resource-group`: Choose one of the available resource groups in your {{site.data.keyword.cloud_notm}} account. Most accounts have a `Default` group. For more information, see [Managing resource groups](https://cloud.ibm.com/docs/account?topic=account-rgs&interface=ui).
    - `datacenter`: Use one of the following. This parameter must match the region that you have selected.
       - `ibm:us-south:dal`
       - `ibm:eu-de:fra`
       - `ibm:eu-gb:lon`
       - `ibm:au-syd:syd`
       - `ibm:jp-tok:tok`
    - `cloud_type`:
       - `ibm`: For fully managed account instances (default).
       - `aws_vpc`: For customer-owned account instances.
    - `use_case_template`: You can provision the Lite plan instance based on three use cases. The valid values accepted by the parameter are ai (Generative AI), workloads (Data Engineering workloads), and performance (High Performance BI). The default value is `workloads`.

         For availability and general information related to customer-owned account deployed instances, contact your IBM sales representative or [open a support ticket](https://cloud.ibm.com/unifiedsupport/cases/form).
         {: note}

    Example:

    ```bash
    ibmcloud resource service-instance-create watsonx.data-abc lakehouse lakehouse-lite us-south -g Default -p '{"datacenter": "ibm:us-south:dal","cloud_type": "ibm"}'
    ```
    {: codeblock}

4. Check the status of the new instance.

    ```bash
    ibmcloud resource service-instance <instance-name>
    ```
    {: codeblock}

## Open the web console
{: #open_console-2}
{: step}


1. From the **Resource list** page, under the **Databases** category, you can see that the status for your instance as, **Provision in progress**. Click the {{site.data.keyword.lakehouse_short}} instance link when the status changes to **Active**.

1. Click **Open web console** and provide the Multi-Factor Authentication (MFA) details to launch the {{site.data.keyword.lakehouse_short}} Console. A **Preparing watsonx.data** page is displayed until your instance is completely provisioned.

1. After the provisioning process is complete, you can view the **Welcome to {{site.data.keyword.lakehouse_short}}** landing page.

## Reference
{: #gs_ns_2}

To explore the features of {{site.data.keyword.lakehouse_short}} web console, see [Lite plan](watsonxdata?topic=watsonxdata-tutorial_hp_intro).
