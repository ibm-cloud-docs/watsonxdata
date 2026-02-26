---

copyright:
  years: 2022, 2026
lastupdated: "2026-02-26"

keywords: watsonx.data, lite, plan, instance

subcollection: watsonxdata

---


{{site.data.keyword.attribute-definition-list}}


{:step: data-tutorial-type="step"}
{:shortdesc: .shortdesc}


# {{site.data.keyword.lakehouse_short}} Lite plan
{: #tutorial_prov_lite_1}


The **Lite** plan allows you to provision an {{site.data.keyword.lakehouse_full}} instance that is free to use, with capacity limit of 500 Resource Units, and time frame limit of 30 days. You can use the account to explore and familiarize yourself with {{site.data.keyword.lakehouse_short}}. For more information about the features and limitations of Lite plan, see [Lite plan](/docs/watsonxdata?topic=watsonxdata-getting-started#lite-plan-1){: external}.
{: shortdesc}


The {{site.data.keyword.lakehouse_short}} Lite plan instance is configured based on the **Generative AI** use case.  The provisioned instance includes Presto (Java), Milvus, and Spark, a read-only sample IBM COS storage that is associated to the Presto engine, and sample worksheet with `GoSales` data in it.



After provisioning the Lite plan instance, you can monitor the resource unit usage from the **Billing and Usage** page available in the {{site.data.keyword.lakehouse_short}} console. For more information, see [Billing and Usage](/docs/watsonxdata?topic=watsonxdata-manage_bill).


Only one active Lite plan instance is allowed for IBM Cloud trial or paid account users. However, if the existing Lite plan instance is deleted before consuming the 500 RUs, a new instance can be created and the remaining RUs can be consumed. Paid account users can create multiple Lite plan instances in different [resource groups](https://cloud.ibm.com/docs/account?topic=account-rgs&interface=ui). If the account has multiple Lite instances active at the same time, the resource unit consumption for the account will be the sum of resource units consumed by each individual instance.

When the limit is reached, any active Lite plan instance owned by the account is disabled and new Lite plan instances cannot be created.


To access all the features and functionalities without resource or time limit, you must have an Enterprise {{site.data.keyword.lakehouse_short}} instance in the paid IBM Cloud account.
In this tutorial, you learn how to provision {{site.data.keyword.lakehouse_short}} instance (Lite plan) and explore its features.

* [Provisioning {{site.data.keyword.lakehouse_short}} Lite plan through UI](#hp_view_1)

* [Provisioning {{site.data.keyword.lakehouse_short}} Lite plan through CLI](#create-lite-cli)

* [Provisioning {{site.data.keyword.lakehouse_short}} Lite plan through Terraform module](#create-lite-terra)







## Before you begin
{: #hp_byb}

To provision {{site.data.keyword.lakehouse_short}} Lite plan instance, you must have a trial account (or a paid account) on the IBM Cloud.
Trial IBM Cloud accounts can have only one resource group.


## Provisioning {{site.data.keyword.lakehouse_short}} Lite plan through UI
{: #hp_view_1}

Perform the following steps to provision a Lite plan instance:


1. Go to the [{{site.data.keyword.lakehouse_short}} provisioning](https://cloud.ibm.com/watsonxdata) page.

1. Click the **Create** tab. Select IBM Cloud as the cloud platform to deploy {{site.data.keyword.lakehouse_short}}.

    In the **Management method** field, **Fully managed** is the default option, which indicates that IBM manages all the network complexities.
    {: note}


    Click **About** tab and read through to understand about the resource units consumed by engine/service, and estimate your consumption of 500 RUs in the {{site.data.keyword.lakehouse_short}} Lite plan instance.
    {: note}


1. In the **Select a pricing plan** field, select **Lite**.

1. Select a location from the **Choose a location** drop-down list.

1. Enter the service name. The service name can be any string. This service name is used in the web console to identify the new deployment.

1. Select the resource group.

    IBM Cloud trial accounts can have only one resource group.
    {: note}


1. Optional: Enter the tags and access management tags.

1. In the **Summary** page, review the license agreement and select the checkbox to agree.


1. Click **Create**. The **Preparing {{site.data.keyword.lakehouse_short}}** page opens that displays the progress. The {{site.data.keyword.lakehouse_short}} Console opens after provisioning is complete.


The Lite plan is limited to a maximum of one Presto engine, one Spark engine (small size, single node) or Milvus service with starter size (1.25 RUs per hour) or all three. You must delete the existing one to add a new one from **Infrastructure manager > Add components**.

You can have only one active Spark engine in the {{site.data.keyword.lakehouse_short}} instance. To set up a new Spark engine, you must first remove the existing one and then provision a new one. For information about how to provision a serverless Spark engine, see [Provisioning a serverless Spark engine](/docs/watsonxdata?topic=watsonxdata-serv_spl_engine).
{: note}




## Provisioning {{site.data.keyword.lakehouse_short}} Lite plan through CLI
{: #create-lite-cli}

Perform the following steps to provision a Lite plan instance by using CLI.

1. Log in to `cloud.ibm.com`.

   ```bash
   ibmcloud login --sso -a https://cloud.ibm.com
   ```
   {: codeblock}

2. Select an account in which you want to create an instance.

3. Create a new formation.

    ```bash
    ibmcloud resource service-instance-create <instance-name> lakehouse <plan-id> <region> -g <resource-group> -p '{"datacenter": "<data-center>","cloud_type": "<cloud-type>","use_case": "<use_case_template>"}'
    ```
    {: codeblock}

    - `instance-name`: Name of the instance. For example, watsonx.data-abc.
    - `lakehouse`: {{site.data.keyword.lakehouse_short}} service.
    - `plan-id` : The plan-id is `lakehouse-lite` for regions `eu-de`, `us-east`, `us-south`, and `jp-tok`.
    - `region`: The available regions are `eu-de`, `us-south`, and `jp-tok`.
    - `resource-group`: Choose one of the available resource groups in your {{site.data.keyword.cloud_notm}} account. Most accounts have a `Default` group. For more information, see [Managing resource groups](https://cloud.ibm.com/docs/account?topic=account-rgs&interface=ui).
    - `datacenter`: Use one of the following. This parameter must match the region that you have selected.
       - `ibm:us-south:dal`
       - `ibm:eu-de:fra`

       

       
       

       - `ibm:jp-tok:tok`
    - `cloud_type`:
       - `ibm`: For fully managed account instances (default).
       - `aws_vpc`: For customer-owned account instances.
    - `use_case_template`: The default value accepted by the parameter is `ai (Generative AI)`.

       

         For availability and general information related to customer-owned account deployed instances, contact your IBM sales representative or [open a support ticket](https://cloud.ibm.com/unifiedsupport/cases/form).
         {: note}

    Example 1 : Provision a Lite plan in `us-south` region.

    ```bash
    ibmcloud resource service-instance-create watsonx.data-abc lakehouse lakehouse-lite us-south -g Default -p '{"datacenter": "ibm:us-east:wdc", "use_case": "ai"}'
    ```
    {: codeblock}

    

4. Check the status of the new instance.

    ```bash
    ibmcloud resource service-instance <instance-name>
    ```
    {: codeblock}


## Provisioning {{site.data.keyword.lakehouse_short}} Lite plan through Terraform module
{: #create-lite-terra}

You can provision a {{site.data.keyword.lakehouse_short}} Lite plan instance by using a pre-built, open-source, enterprise-ready Terraform module. This method uses [Terraform IBM Modules (TIM)](https://cloud.ibm.com/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-about-tim), which are curated collections of Terraform modules that simplify creating, managing, and versioning complex, compliant environments on IBM Cloud.

### About the {{site.data.keyword.lakehouse_short}} Terraform module
{: #create-lite-terra-1}

The [{{site.data.keyword.lakehouse_short}} module](https://registry.terraform.io/modules/terraform-ibm-modules/watsonx-data/ibm/latest) is a purpose-built Terraform module that follows secure-by-default principles and aligns with IBM Cloud best practices. The module provides the following capabilities:

- Standardized method for creating and working with IBM {{site.data.keyword.lakehouse_short}} instances
- Comprehensive documentation with README files and examples
- Multiple deployment scenarios through basic, advanced, and existing instance examples
- Controlled versioning for safe updates and easier dependency management
- Enterprise-ready configurations that are secure, scalable, and compliant

### Deploying the module
{: #create-lite-terra-2}

To deploy the {{site.data.keyword.lakehouse_short}} Lite plan by using this Terraform module, complete the steps in [Deploying a Terraform IBM Module by using Terraform CLI](https://cloud.ibm.com/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-deploy-tim-module).

The deployment process includes the following steps:

1. Verify that you have the required prerequisites: Terraform CLI and IBM Cloud API key.
2. Create the Terraform configuration based on the code and examples provided.
3. Configure input variables for your deployment.
4. Run `terraform init` to download required providers and modules.
5. Run `terraform plan` to preview the changes that Terraform will make to your infrastructure.
6. Run `terraform apply` to provision your {{site.data.keyword.lakehouse_short}} lite plan instance.



## Reference
{: #gs_ns_2}

To explore the features of {{site.data.keyword.lakehouse_short}} web console, see [Lite plan](/docs/watsonxdata?topic=watsonxdata-tutorial_hp_intro).
