---

copyright:
  years: 2022, 2024
lastupdated: "2024-04-30"

keywords: watsonx.data, data ingestion, source file

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

# Integrating with IBM Knowledge Catalog
{: #integrate_wkc}

Integrating {{site.data.keyword.lakehouse_full}} with IBM Knowledge Catalog provides self-service access to data assets for knowledge workers who need to use those data assets to gain insights.
{: shortdesc}

## About this task
{: #abt_tsk}

IBM Knowledge Catalog provides a secure enterprise catalog management platform that is supported by a data governance framework. A catalog connects people to the data and knowledge that they need.

A catalog is how you share assets across your enterprise:

- Collaborators in a catalog have access to data assets without needing separate credentials or being able to see the credentials.

- An asset in a catalog consists of metadata about data, including how to access the data, the data format, the classification of the asset, which collaborators can access the data and other types of metadata that describe the data.

## Procedure
{: #Prcdre1}

To integrate {{site.data.keyword.lakehouse_short}} with IBM Knowledge Catalog, complete the following steps:

1. Log in to {{site.data.keyword.lakehouse_short}} console.
2. From the navigation menu, select Access control.
3. Click the Integrations tab.
4. Click Integrate service. The Integrate service window opens.
5. In the Integrate service window, provide the following details:

   | Field           | Description        |
   |------------------|--------------------|
   | Service     | Select the service (Knowledge Catalog) to be integrated. |
   | Bucket catalogs      | Select the bucket catalogs for Knowledge Catalog governance. |
   | WKC endpoint            | Specify the Knowledge Catalog endpoint URL. |
   {: caption="Table 1." caption-side="bottom"}

6. Click Integrate.
   The service is integrated and listed in the Access Control page.

   You can transform or mask data in {{site.data.keyword.lakehouse_short}} based on the data protection rules that are defined in the IBM Knowledge Catalog.
