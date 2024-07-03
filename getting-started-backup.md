---

copyright:
  years: 2022, 2024
lastupdated: "2024-07-03"

keywords: lakehouse, watsonx data, provision, endpoint, resource
subcollection: watsonxdata

content-type: tutorial
services:
account-plan: paid
completion-time: 20m

---


{{site.data.keyword.attribute-definition-list}}

# Getting started with {{site.data.keyword.lakehouse_short}}
{: #getting-started}
{: toc-content-type="tutorial"}
{: toc-services=""}
{: toc-completion-time="20m"}


{{site.data.keyword.lakehouse_full}} is a data management solution for collecting, storing, querying, and analyzing all your enterprise data with a single unified data platform. It provides a flexible and reliable platform that is optimized to work on open data formats.
This tutorial is a short introduction to using a {{site.data.keyword.lakehouse_short}} deployment.
{: shortdesc}

For more information about the developer edition of {{site.data.keyword.lakehouse_short}} and {{site.data.keyword.lakehouse_short}} on Red Hat OpenShift, see [{{site.data.keyword.lakehouse_full}}](https://www.ibm.com/docs/en/watsonxdata/1.1.x).

For more information about using {{site.data.keyword.lakehouse_full}} on Cloud Pak for Data, see [{{site.data.keyword.lakehouse_full}} on Cloud Pak for Data](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.8.x?topic=services-watsonxdata).

## Before you begin
{: #prereqs}

You need to have an [{{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/registration){: external}.

The access to provision IBM Cloud resources is governed by using [IAM access](https://cloud.ibm.com/docs/account?topic=account-userroles&interface=ui) and [account management services](https://cloud.ibm.com/docs/account?topic=account-account-services&interface=ui). You must have **Administrator** privileges to access the resource group in which you need to create the resources.
{: note}




## Review resource unit consumption
{: #hp_view_lit}
{: step}

To understand about the resource unit consumption for the components in the {{site.data.keyword.lakehouse_short}}instance, follow the steps:

1. Go to the [{{site.data.keyword.cloud_notm}} catalog](https://cloud.ibm.com/catalog) page, find the **{{site.data.keyword.lakehouse_short}}** tile and click it. The [**{{site.data.keyword.lakehouse_short}}** **{{site.data.keyword.Bluemix_short}} catalog**](https://cloud.ibm.com/watsonxdata) page opens.

1. Select the **About** tab.

1. You can read through the **Summary** and **Features**.

1. In the **Pricing estimator**, provide the following inputs and review the **Estimate summary** to assess the hourly cost for the resource units.


   | Field | Description |
   |--------------------------|----------------|
   |Select platform |Select the platform.|
   |License |Select the license plan.|
   |Support services|Includes the necessary access control and metastore. The resource unit quantity is visible on the right.|
   |Engine/Service 1|Select the engine or service of your choice.|
   |If you select **Presto**|**a**. Select the coordinated node type and number of coordinated nodes. The resource unit quantity is visible on the right. \n **b**. Select the worker node type and number of worker nodes. The resource unit quantity is visible on the right.|
   |If you select **Milvus**|Select the size of your choice. The resource unit quantity is visible on the right.|
   {: caption="Table 1. Pricing estimator" caption-side="bottom"}

## Provision an instance
{: #create}
{: step}

* [Provision an instance through UI](#create-by-ui)
* [Provision an instance through CLI](#create-by-cli)

### Provision an instance through UI
{: #create-by-ui}

1. Go to the [{{site.data.keyword.cloud_notm}} catalog](https://cloud.ibm.com/catalog) page.

2. Find the **{{site.data.keyword.lakehouse_short}}** tile and click it. You are redirected to the provisioning page.

3. Select the cloud platform (IBM Cloud or Amazon Web Services) you want to deploy {{site.data.keyword.lakehouse_short}}.

4. In the **Management method** field, **Fully managed** is the default option, which indicates that IBM manages all the network complexities.

5. Select a location from the list of available locations for {{site.data.keyword.lakehouse_short}} service.

6. Enter the service name. The service name can be any string. This service name is used in the web console to identify the new deployment.

7. Select a resource group. If you are organizing your services into resource groups, specify the resource group.

8. Enter a tag name.

9. Enter the access management tags.

   <!-- 1. Select the type of network endpoints that is used for accessing the service.
   a. **Public endpoint only** - Public endpoints provide a connection to your deployment on the public network (single endpoint).
   b. **Private endpoint only** - Private endpoints route traffic through the IBM Cloud Private network (single endpoint).
   c. **Both public and private endpoints** - Public endpoints provide a connection to your deployment on the public network. Private endpoints route traffic through the IBM Cloud Private network. (Two separate endpoints). -->

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
    ibmcloud resource service-instance-create <instance-name> lakehouse lakehouse-enterprise <region> -g Default -p <cloud_type> '{"datacenter": ""}'`
    ```
    {: codeblock}

    - `instance-name:` name of the formation. For example, watsonx.data-abc.
    - `lakehouse-enterprise:` Plan ID
    - `lakehouse:` {{site.data.keyword.lakehouse_short}} service
    - `datacenter:` Required parameter. For example, `ibm:us-south:dal`, `aws:us-west-2`, `aws:us-east-1`, `aws:eu-central-1`, `ibm:us-east:wdc`, and `ibm:eu-de:fra`.
    - `cloud_type:` the type of cloud environment you want to use. For Blueray service instance creation, cloud type is `aws_vpc`.
    - Regions are `eu-de`, `us-east`, `us-south` and `jp-tok`.

    Example:

    ```bash
    ibmcloud resource service-instance-create watsonx.data-abc lakehouse lakehouse-enterprise us-south -g Default -p aws_vpc '{"datacenter": "ibm:us-south:dal"}'
    ```
    {: codeblock}

4. Check the status of the new instance.

    ```bash
    ibmcloud resource service-instance <instance-name>
    ```
    {: codeblock}

## Open the web console
{: #open_console}
{: step}

1. Go to **Resource list** **>** **Databases**.

2. Click your {{site.data.keyword.lakehouse_short}} instance link. The service instance page opens.

3. Click **Open web console**. The {{site.data.keyword.lakehouse_short}} web console opens.

    <!-- 1. Log in to the console with your IBMid and password. The {{site.data.keyword.lakehouse_short}} web console opens. -->

## Next steps
{: #gs_ns}

To quickly get started with the {{site.data.keyword.lakehouse_short}} web console by configuring the infrastructure components, see [Quick start {{site.data.keyword.lakehouse_short}} console](watsonxdata?topic=watsonxdata-quick_start).

Once you complete quick start, Resource Unit consumption begins and will be reported for billing.
If you do not complete the quick start and provision support services, Resource Units are not consumed and reported for billing.
If no Resource Units are consumed within seven (7) days after an instance creation, the unused instance is deleted, after which a new instance can be re-created. For more information, see [Provisioning an instance](#create-by-ui).
{: important}
