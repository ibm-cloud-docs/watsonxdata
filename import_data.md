---

copyright:
  years: 2022, 2023
lastupdated: "2023-10-11"

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

1. There are two ways to import a file to create table. Select the required option:

    * Option 1: To import file to any available schema under a catalog, do the following steps:

        a. Click **Create** drop-down.

        b. Click **Create table from file**. The **Create table from a file** page opens.

        c. Go to step 5.

    * Option 2: To import file to a particular schema under the catalog, do the following steps:

        a. Select a schema under a catalog where you want to import a file to create table.

        b. Click the overflow menu of the selected schema and select **Create table from a file**. The **Create table from a file** page opens.

1. Follow the steps in the [Creating tables](watsonxdata?topic=watsonxdata-create_table) topic to complete importing the file.



<!--
1. Select the engine from the **Engine** drop-down. Catalogs that are associated with the selected engine are listed.

1. Click **Create table from file**. The **Create table from a file** page opens.
    You can also import a file into a particular schema. To do that, follow the steps:

      a. Select a schema under a catalog where you want to import a file to create table.
      b. Click the overflow menu of the selected schema and select **Create table from a file**. The **Create table from a file** page opens.

1. Follow the steps in the [Creating tables](watsonxdata?topic=watsonxdata-create_table) topic to complete importing the file. -->
