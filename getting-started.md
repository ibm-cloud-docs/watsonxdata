---

copyright:
  years: 2022, 2025
lastupdated: "2026-02-11"

keywords: lakehouse, watsonx data, provision, endpoint, resource
subcollection: watsonxdata



---


{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.lakehouse_short}} enterprise plan
{: #getting-started_1}



{{site.data.keyword.lakehouse_full}} is a data management solution for collecting, storing, querying, and analyzing all your enterprise data with a single unified data platform. It provides a flexible and reliable platform that is optimized to work on open data formats.
This tutorial is a short introduction to using a {{site.data.keyword.lakehouse_short}} deployment.
{: shortdesc}

For more information about the developer edition of {{site.data.keyword.lakehouse_short}} and {{site.data.keyword.lakehouse_short}} on Red Hat OpenShift, see [{{site.data.keyword.lakehouse_full}}](https://www.ibm.com/docs/en/watsonx/watsonxdata/2.2.x).

For more information about using {{site.data.keyword.lakehouse_short}} on IBM Software Hub. For more information, see [{{site.data.keyword.lakehouse_full}} on IBM Software Hub](https://www.ibm.com/docs/en/software-hub/5.2.x).

## Before you begin
{: #prereqs}

You need to have a paid [{{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/registration){: external}.

The access to provision IBM Cloud resources is governed by using [IAM access](https://cloud.ibm.com/docs/account?topic=account-userroles&interface=ui) and [account management services](https://cloud.ibm.com/docs/account?topic=account-account-services&interface=ui). You must have **Administrator** privileges to provision a {{site.data.keyword.lakehouse_short}} instance.
{: note}

## Provision an instance
{: #create}
{: step}

* [Provision an instance through UI](#create-by-ui)
* [Provision an instance through CLI](#create-by-cli)
* [Provisioning an instance through Terraform module](#create-by-tf-module)

### Provision an instance through UI
{: #create-by-ui}

1. Go to the [{{site.data.keyword.cloud_notm}} catalog](https://cloud.ibm.com/catalog) page.

2. Find the **{{site.data.keyword.lakehouse_short}}** tile and click it. You are redirected to the provisioning page.

3. Select the cloud platform (IBM Cloud or Amazon Web Services) you want to deploy {{site.data.keyword.lakehouse_short}}.

4. Select the pricing plan as **Enterprise** from the **Select a pricing plan** options.



5. Select a location from the list of available locations for {{site.data.keyword.lakehouse_short}} service.

6. Enter the service name. It can be any string and is used in the web console to identify the new deployment.

7. Select a resource group. If you are organizing your services into resource groups, specify the resource group.

8. Enter a tag name.

9. Enter the access management tags.

   

10. Click **Create**.

    After you click **Create**, the system displays a message to say that the instance is being provisioned, which returns you to the **Resource list**. From the **Resource list**, under **Databases** category, you see that the status for your instance is, `Provision in progress`.

11. When the status changes to `Active`, select the instance.

### Provision an instance through CLI
{: #create-by-cli}

1. Log in to `cloud.ibm.com`.

   ```bash
   ibmcloud login --sso -a https://cloud.ibm.com
   ```
   {: codeblock}

2. Select an account on which you want to create an instance.

3. Create a new formation.

    ```bash
    ibmcloud resource service-instance-create <instance-name> lakehouse <plan-id> <region> -g <resource-group> -p '{"datacenter": "<data-center>","cloud_type": "<cloud-type>"}'
    ```
    {: codeblock}

    - `instance-name`: Name of the instance. For example, watsonx.data-abc.
    - `lakehouse`: {{site.data.keyword.lakehouse_short}} service
    - `plan-id` : The plan-id is `lakehouse-enterprise` for regions `eu-de`, `us-east`, `us-south`, `jp-tok`, and `eu-gb`. It must be `lakehouse-enterprise-mcsp` for `au-syd`, `ca-tor` regions.
    - `region`: The available regions are `eu-de`, `us-east`, `us-south`, `jp-tok`, `eu-gb`, `au-syd`, and `ca-tor`.
    - `resource-group`: Choose one of the available resource groups in your {{site.data.keyword.cloud_notm}} account. Most accounts have a `Default` group. For more information, see [Managing resource groups](https://cloud.ibm.com/docs/account?topic=account-rgs&interface=ui).
    - `datacenter`: Use one of the following. This parameter must match the region that you have selected.
       - `ibm:us-south:dal`
       - `ibm:us-east:wdc`
       - `ibm:eu-de:fra`
       - `ibm:eu-gb:lon`
       - `ibm:au-syd:syd`
       - `ibm:ca-tor:tor`
       - `ibm:jp-tok:tok`
    - `cloud_type`:
       - `ibm`: For fully managed account instances (default).
       - `aws_vpc`: For customer-owned account instances.

         For availability and general information related to customer-owned account deployed instances, contact your IBM sales representative or [open a support ticket](https://cloud.ibm.com/unifiedsupport/cases/form).
         {: note}

    Example 1 : Provision an enterprise plan in `us-south` region.

    ```bash
    ibmcloud resource service-instance-create watsonx.data-abc lakehouse lakehouse-enterprise us-south -g Default -p '{"datacenter": "ibm:us-south:dal","cloud_type": "ibm"}'
    ```
    {: codeblock}

    Example 2 : Provision an enterprise plan in `Sydney` region.

    ```bash
    ibmcloud resource service-instance-create <instance-name> lakehouse lakehouse-enterprise-mcsp au-syd -g Default -p '{"datacenter": "ibm:au-syd:syd"}'
    ```
    {: codeblock}

4. Check the status of the new instance.

    ```bash
    ibmcloud resource service-instance <instance-name>
    ```
    {: codeblock}

### Provisioning an instance through Terraform module
{: #create-by-tf-module}

You can provision an instance by using a pre-built, open-source, enterprise-ready Terraform module. This method uses [Terraform IBM Modules (TIM)](https://cloud.ibm.com/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-about-tim), which are curated collections of Terraform modules that simplify creating, managing, and versioning complex, compliant environments on IBM Cloud.

#### About the {{site.data.keyword.lakehouse_short}} Terraform module
{: #create-by-tf-module1}

The [{{site.data.keyword.lakehouse_short}} module](https://registry.terraform.io/modules/terraform-ibm-modules/watsonx-data/ibm/latest) is a purpose-built Terraform module that follows secure-by-default principles and aligns with IBM Cloud best practices. The module provides the following capabilities:

- Standardized method for creating and working with IBM {{site.data.keyword.lakehouse_short}} instances
- Comprehensive documentation with README files and examples
- Multiple deployment scenarios through basic, advanced, and existing instance examples
- Controlled versioning for safe updates and easier dependency management
- Enterprise-ready configurations that are secure, scalable, and compliant

#### Deploying the module
{: #create-lite-tf-module2}

To deploy the {{site.data.keyword.lakehouse_short}} enterprise plan by using this Terraform module, complete the steps in [Deploying a Terraform IBM Module by using Terraform CLI](https://cloud.ibm.com/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-deploy-tim-module).

The deployment process includes the following steps:

1. Verify that you have the required prerequisites: Git CLI, Terraform CLI, and IBM Cloud API key.
2. Clone the GitHub repository that contains the Terraform module.
3. Create a `terraform.tfvars` file to define input variables for your deployment.
4. Run `terraform init` to download required providers and modules.
5. Run `terraform plan` to preview the changes that Terraform will make to your infrastructure.
6. Run `terraform apply` to provision your {{site.data.keyword.lakehouse_short}} instance.



### Provisioning Virtual Private Endpoint (VPE) enabled instance
{: #create-by-VPE}

You can provision an IBM {{site.data.keyword.lakehouse_short}} instance with VPE enabled to connect your IBM {{site.data.keyword.lakehouse_short}} instance privately and securely to resources in your Virtual Private Cloud (VPC), eliminating exposure to the public internet. This configuration is supported in the following regions:

* Dallas (us-south)
* Washington DC (us-east)
* Frankfurt (eu-de)
* Sydney (au-syd)
* Toronto (ca-tor)

Currently, enabling VPE during provisioning requires adding the `vpe_required` parameter only for Dallas, Washington DC, and Frankfurt. Other regions such as Toronto and Sydney do not require this parameter. This is a temporary behavior and will be standardized in a future release.


Examples:

Region: Dallas


```bash
ibmcloud resource service-instance-create <instance_name> lakehouse lakehouse-enterprise us-south -g Default -p '{"cloud_type": "ibm", "region": "us-south", "datacenter": "ibm:us-south:dal", "vpe_required":"true"}'
```
{: codeblock}

Region: Frankfurt

```bash
ibmcloud resource service-instance-create <instance-name> lakehouse lakehouse-enterprise eu-de -g Default -p '{"cloud_type": "ibm", "region": "eu-de", "datacenter": "ibm:eu-de:fra", "vpe_required":"true"}'
```
{: codeblock}

Region: Washington DC

```bash
ibmcloud resource service-instance-create <instance_name> lakehouse lakehouse-enterprise us-east -g Default -p '{"cloud_type": "ibm", "region": "us-east", "datacenter": "ibm:us-east:wdc", "vpe_required":"true"}'
```
{: codeblock}

- `instance-name`: Name of the instance. For example, watsonx.data-abc.
- `lakehouse`: {{site.data.keyword.lakehouse_short}} service
- `plan-id` : The plan-id is `lakehouse-enterprise` for regions `eu-de`, `us-east`, `us-south`, `au-syd`, and `ca-tor`regions.
- `region`: The available regions are `eu-de`, `us-east`, `us-south`, `au-syd`, and `ca-tor`.
- `datacenter`: Use one of the following. This parameter must match the region that you have selected.
   - `ibm:us-south:dal`
   - `ibm:us-east:wdc`
   - `ibm:eu-de:fra`
   - `ibm:au-syd:syd`
   - `ibm:ca-tor:tor`
- `cloud_type`:
   - `ibm`: For fully managed account instances (default).
   - `vpe_required`: This parameter must be set to `True` for `eu-de`, `us-east`, `us-south`. Toronto and Sydney do not require this parameter.



## Open the web console
{: #open_console}
{: step}

1. Go to **Resource list** **>** **Databases**.

2. Click your {{site.data.keyword.lakehouse_short}} instance link. The service instance page opens.

3. Click **Open web console**. The {{site.data.keyword.lakehouse_short}} web console opens.

    

## Next steps
{: #gs_ns}

To quickly get started with the {{site.data.keyword.lakehouse_short}} web console by configuring the infrastructure components, see [Quick start {{site.data.keyword.lakehouse_short}} console](/docs/watsonxdata?topic=watsonxdata-quick_start_213).

After you complete quick start, Resource unit consumption is accounted and billing is started.
If no Resource Units are consumed within seven (7) days after an instance creation, the unused instance is deleted, after which a new instance can be re-created. For more information, see [Provisioning an instance](#create-by-ui).
{: important}
