---

copyright:
  years: 2022, 2025
lastupdated: "2025-05-20"

keywords: lakehouse, semantic automation, {{site.data.keyword.lakehouse_short}}, data enrichment, register

subcollection: watsonxdata

---

{:javascript: #javascript .ph data-hd-programlang='javascript'}
{:java: #java .ph data-hd-programlang='java'}
{:ruby: #ruby .ph data-hd-programlang='ruby'}
{:php: #php .ph data-hd-programlang='php'}
{:python: #python .ph data-hd-programlang='python'}
{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:video: .video}

# Registering and activating semantic layer
{: #sal_register}

To activate semantic enrichment in {{site.data.keyword.lakehouse_full}}, you must have a registered IBM Knowledge Catalog in your IBM Cloud account. Currently, this is available only in the `us-south` region.

## Before you begin
{: #sal_registerbyb}

To register and enable semantic layer in {{site.data.keyword.lakehouse_short}}, make sure that the following are available.
- [API key](https://cloud.ibm.com/iam/apikeys) of the cluster.
- IBM Knowledge Catalog instance within your IBM Cloud account.
-

## Procedure
{: #sal_registerprcdre}

1. Log in to {{site.data.keyword.lakehouse_short}} console.
1. From the navigation menu, select **Configurations** and click **Semantic layer integration** tile.
1. Click **Add a registration**.
1. For Lite plan users, enter the API key in the API key field of **Add registration** window.

   You can generate and copy a new API key from the `Manage->Access(IAM)->API keys` of the IBM Cloud cluster.
   {: note}

   Lite plan users can access a 30 days trial version only.
   {: note}

1. Select a **Presto engine** from the engine drop-down list.
1. Click **Register**. Semantic automation layer is active.

1. For Enterprise plan users, enter the API key in the API key field of **Add registration** window.

   You can generate and copy a new API key from the `Manage->Access(IAM)->API keys` of the IBM Cloud cluster.
   {: note}

1. Select a **Presto engine** from the engine drop-down list.
1. Enter Cloud Object Storage (COS) details:
   - Cloud Object Storage (COS) CRN
   - Select a Cloud Object Storage (COS) type

1. Click **Register**. Semantic automation layer is active.

## Related API
{: #salreg_api}

For information on related API, see
* [Get SAL integrations](https://cloud.ibm.com/apidocs/watsonxdata#get-sal-integration)
* [Create SAL integration with wxd](https://cloud.ibm.com/apidocs/watsonxdata#create-sal-integration)
* [Delete SAL-wxd integration](https://cloud.ibm.com/apidocs/watsonxdata#delete-sal-integration)
* [Update SAL-wxd integration](https://cloud.ibm.com/apidocs/watsonxdata#update-sal-integration)
