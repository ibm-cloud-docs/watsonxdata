---

copyright:
  years: 2022, 2024
lastupdated: "2024-08-25"

keywords: lakehouse, engine, watsonx.data
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

# Configuring Presto resource groups
{: #conf_rcrs_grp}

You can configure one or more Presto resource groups in {{site.data.keyword.lakehouse_short}}.
{: shortdesc}

To configure resource groups:

1. Log in to {{site.data.keyword.lakehouse_short}} console.
1. From the navigation menu, go to **Configurations**.
1. Click the **Presto resource groups** tile.
   The **Presto resource groups** window opens.
1. Click **Add Resource Group**.
1. From the **Add Resource Group** window, browse and select a resource group JSON file.
   Alternatively, you can drag and drop a resource group file.

   The uploaded JSON file structure must match with the sample resource group file structure. To download the sample file, click **Download sample resource group**. The maximum allowed size of a file is 2 MB and the only file format that is supported is `.json`.
   {: important}

   For more information about the resource group properties that you can define in the JSON file, see [Resource group properties](watsonxdata?topic=watsonxdata-resource_grp_pptys).
1. Click **Add** to add the resource group.

   To delete a resource group, go to the overflow menu of the resource group and click **Delete**. A confirmation box opens. Click **Delete** to confirm deletion. You cannot delete a resource group if it is assigned to an engine.
   {: note}

1. To assign the resource group to engines, click the overflow menu of the resource group and select **Assign**.
1. Select one or more Presto engines from the **Available engines** section and click **Assign**.
   A confirmation box opens.

   If you click **Confirm**, the engines restart, and any ongoing queries of the data sources that are associated to the engines are terminated. You can have only one resource group assigned to an engine.
   {: note}

1. Click **Confirm** to complete the configuration.

## Unassigning resource group from engines
{: #unassign_rcrs_grp}

You can unassign a resource group from engines.
{: shortdesc}

To unassign:

1. Click the overflow menu of the resource group and select **Unassign**.
1. From the **Currently assigned engines** section, select one or more engines that you want to unassign the resource group from.
1. Click **Unassign**. A confirmation box opens.

    If you click **Confirm**, the engines restart, and any ongoing queries of the data sources that are associated to the engines are terminated.
    {: note}

1. Click **Confirm** to unassign.