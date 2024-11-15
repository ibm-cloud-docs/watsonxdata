---

copyright:
  years: 2022, 2024
lastupdated: "2024-11-06"

keywords: lakehouse, watsonx.data, query optimizer, install

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

# Activating Query Optimizer Manager
{: #install_optimizer}

To enable **Query Optimizer** in {{site.data.keyword.lakehouse_full}}, you must activate **Query Optimizer Manager** through the web console.

## Before you begin
{: #install_optimizerbyb}

To enable **Query Optimizer**, make sure at least one Presto (C++) engine is provisioned and active within your {{site.data.keyword.lakehouse_short}} instance.

## Procedure
{: #install_optimizerprcdre}

1. Log in to {{site.data.keyword.lakehouse_short}} console.
1. From the navigation menu, select **Configurations** and click **Query Optimizer Manager** tile.
1. Click **Activate** and confirm the activation and restarting of the engines in the **Activate query optimizer** window.

   **Query Optimizer** takes approximately 20 minutes to deploy and sync over metadata for all Hive and Iceberg catalogs and schemas. This time may vary based on the metadata size to be synced.
   {: note}

   Verify that all expected tables have been synced. If tables are found missing during the automatic syncing process, you can manually sync the tables. See [Manually syncing Query Optimizer]({{site.data.keyword.ref-sync_optimizer_meta-link}}).
   {: note}

   You can click **Cancel activation** to cancel the deployment of **Query Optimizer Manager** during the deployment.
   {: note}
