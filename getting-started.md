---

copyright:
  years: 2022, 2024
lastupdated: "2024-12-14"

keywords: lakehouse, watsonx data, provision, endpoint, resource
subcollection: watsonxdata



---


{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.lakehouse_short}} enterprise plan
{: #getting-started_1}



{{site.data.keyword.lakehouse_full}} is a data management solution for collecting, storing, querying, and analyzing all your enterprise data with a single unified data platform. It provides a flexible and reliable platform that is optimized to work on open data formats.
This tutorial is a short introduction to using a {{site.data.keyword.lakehouse_short}} deployment.
{: shortdesc}

For more information about the developer edition of {{site.data.keyword.lakehouse_short}} and {{site.data.keyword.lakehouse_short}} on Red Hat OpenShift, see [{{site.data.keyword.lakehouse_full}}](https://www.ibm.com/docs/en/watsonxdata/1.1.x).

For more information about using {{site.data.keyword.lakehouse_short}} on IBM Software Hub. For more information, see [{{site.data.keyword.lakehouse_full}} on IBM Software Hub](https://www.ibm.com/docs/SSNFH6_5.1.x)..

## Before you begin
{: #prereqs}

You need to have an [{{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/registration){: external}.

The access to provision IBM Cloud resources is governed by using [IAM access](https://cloud.ibm.com/docs/account?topic=account-userroles&interface=ui) and [account management services](https://cloud.ibm.com/docs/account?topic=account-account-services&interface=ui). You must have **Administrator** privileges to provision a {{site.data.keyword.lakehouse_short}} instance.
{: note}

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
    ibmcloud resource service-instance-create <instance-name> lakehouse lakehouse-enterprise <region> -g <resource-group> -p '{"datacenter": "<data-center>","cloud_type": "<cloud-type>"}'
    ```
    {: codeblock}

    - `instance-name`: Name of the instance. For example, watsonx.data-abc.
    - `lakehouse`: {{site.data.keyword.lakehouse_short}} service
    - `lakehouse-enterprise`: Plan ID
    - `region`: The available regions are `eu-de`, `us-east`, `us-south`, `jp-tok`, `eu-gb`, and `au-syd`.
    - `resource-group`: Choose one of the available resource groups in your {{site.data.keyword.cloud_notm}} account. Most accounts have a `Default` group. For more information, see [Managing resource groups](https://cloud.ibm.com/docs/account?topic=account-rgs&interface=ui).
    - `datacenter`: Use one of the following. This parameter must match the region that you have selected.
       - `ibm:us-south:dal`
       - `ibm:us-east:wdc`
       - `ibm:eu-de:fra`
       - `ibm:eu-gb:lon`
       - `ibm:au-syd:syd`
       - `ibm:jp-tok:tok`
    - `cloud_type`:
       - `ibm`: For fully managed account instances (default).
       - `aws_vpc`: For customer-owned account instances.

         For availability and general information related to customer-owned account deployed instances, contact your IBM sales representative or [open a support ticket](https://cloud.ibm.com/unifiedsupport/cases/form).
         {: note}

    Example:

    ```bash
    ibmcloud resource service-instance-create watsonx.data-abc lakehouse lakehouse-enterprise us-south -g Default -p '{"datacenter": "ibm:us-south:dal","cloud_type": "ibm"}'
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

    

## Next steps
{: #gs_ns}

To quickly get started with the {{site.data.keyword.lakehouse_short}} web console by configuring the infrastructure components, see [Quick start {{site.data.keyword.lakehouse_short}} console](watsonxdata?topic=watsonxdata-quick_start).

After you complete quick start, Resource unit consumption is accounted and billing is started.
If no Resource Units are consumed within seven (7) days after an instance creation, the unused instance is deleted, after which a new instance can be re-created. For more information, see [Provisioning an instance](#create-by-ui).
{: important}
