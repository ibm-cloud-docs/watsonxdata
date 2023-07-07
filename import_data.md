---

copyright:
  years: 2022, 2023
lastupdated: "2023-07-07"

keywords: lakehouse, ingesting data, create table

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

# Creating table from a file
{: #import_data}

Files can also be ingested or imported to {{site.data.keyword.lakehouse_full}} through the overflow menu of schema in the **Data explorer** page to create tables.
{: shortdesc}

1. Log in to the {{site.data.keyword.lakehouse_short}} console.

1. From the navigation menu, select **Data manager**.

1. Select the engine from the **Engine** drop-down. Catalogs that are associated with the selected engine are listed.

1. Select a schema under a catalog where you want to import a file to create table.

1. Click the overflow menu of the selected schema and select **Create table from a file**. The **Create table from a file** page opens.
1. Follow the steps in the [Creating tables](watsonxdata?topic=watsonxdata-create_table) topic to complete importing the file.
