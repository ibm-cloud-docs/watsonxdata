---

copyright:
  years: 2022, 2023
lastupdated: "2023-10-11"

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

## Before you begin
{: #prereqs}

You need to have an [{{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/registration){: external}.

To provision an instance, you must have IBM Cloud permissions for resource creation. For more information about the permissions, see [IAM access](/docs/account?topic=account-userroles).
{: note}

## Provision an instance
{: #create}
{: step}

1. Go to the [{{site.data.keyword.cloud_notm}} catalog](https://cloud.ibm.com/catalog) page.

1. Find the **{{site.data.keyword.lakehouse_short}}** tile and click it. You are redirected to the provisioning page.

1. Select the cloud platform (IBM Cloud or Amazon Web Services) you want to deploy {{site.data.keyword.lakehouse_short}}.

1. Select a location from the list of available locations for {{site.data.keyword.lakehouse_short}} service.

1. Enter the service name. The service name can be any string. This service name is used in the web console to identify the new deployment.

1. Select a resource group. If you are organizing your services into resource groups, specify the resource group.

1. Enter a tag name.

1. Select the type of network endpoints that is used for accessing the service.

   a. **Public endpoint only** - Public endpoints provide a connection to your deployment on the public network (single endpoint).

   b. **Private endpoint only** - Private endpoints route traffic through the IBM Cloud Private network (single endpoint).

   c. **Both public and private endpoints** - Public endpoints provide a connection to your deployment on the public network. Private endpoints route traffic through the IBM Cloud Private network. (Two separate endpoints).

1. Click **Create**.

   After you click **Create**, the system displays a message to say that the instance is being provisioned, which returns you to the **Resource list**. From the **Resource list**, under **Databases** category, you see that the status for your instance is, `Provision in progress`.

1.  When the status changes to `Active`, select the instance.

## Open the web console
{: #open_console}
{: step}

1. Go to **Resource list** **>** **Databases**.

1. Click your {{site.data.keyword.lakehouse_short}} instance link. The service instance page opens.

1. Click **Open web console** to start the web console.

1. Log in to the console with your IBMid and password. The {{site.data.keyword.lakehouse_short}} web console opens.

## Next steps
{: #gs_ns}

To quickly get started with the {{site.data.keyword.lakehouse_short}} web console by configuring the infrastructure components, see [Quick start {{site.data.keyword.lakehouse_short}} console](watsonxdata?topic=watsonxdata-quick_start).
