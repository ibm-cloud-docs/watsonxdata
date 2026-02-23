---

copyright:
  years: 2022, 2025
lastupdated: "2026-02-23"

keywords: lakehouse, web console, watsonx.data

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


# Getting started with the web console
{: #getstarted-console}

If you are logging in to watsonx.data instance for the first time, you will be presented with a quick start wizard. For details about the wizard, see the [Quick start watsonx.data console](/docs/watsonxdata?topic=watsonxdata-quick_start_213){: external}.
{: note}

To start {{site.data.keyword.lakehouse_full}} web console, complete the following steps:
{: shortdesc}

1. Log in to your {{site.data.keyword.cloud_notm}} Account.
2. Go to **Resource list** **>** **Databases**.
3. Click your {{site.data.keyword.lakehouse_full}} instance link. The service instance page opens.
4. Click **Open web console** to load the home page.



The home page provides information about the logged in user, the login timestamp, and region where the {{site.data.keyword.lakehouse_short}} is created.

The home page provides information about the logged in user, the login timestamp, and region where the {{site.data.keyword.lakehouse_short}} is created.

## Homepage tiles
{: #getstarted-console_1}

The Homepage displays tiles that provide quick access to key lakehouse management tasks:

**Architect your lakehouse**
: Define and associate infrastructure components to make your data queryable. Click **Infrastructure manager** to configure engines, catalogs, and storage for your lakehouse environment.

**Ingest data to your lakehouse**
: Securely load data from local, remote files and databases. Click **Data ingestion** to create ingestion jobs that move data into your lakehouse.

**Work with your data**
: Build and run queries against your data, monitor their progress, and save them for reuse. Click **Query workspace** to access the SQL query interface.

**Break down the data silos**
: Work with your data in data visualization tools or your IDE. Click **BI tools** to connect business intelligence applications or **VS Code** to integrate with your development environment.

These tiles are available across all {{site.data.keyword.lakehouse_short}} deployment environments, including SaaS, AWS MCSP, and Lite instances.

## Additional information on the home page
{: #getstarted-console_2}

The home page also displays the following informational panels:

- **Welcome to IBM watsonx.data**: Browse recommended resources to get up to speed quickly, catch up on what's new, and discover what you can achieve through integrations with watsonx.data.
- **Infrastructure components**: View counts of engines/services, catalogs, storage, and data sources configured in your environment.
- **Recent tables**: Access recently used tables from the data manager.
- **Recent ingestion jobs**: Monitor the status of recent data ingestion operations.
- **Saved worksheets**: Access your saved SQL queries and worksheets.
- **Recent queries**: View your query history and execution status.

From the home page, you can go to the **Infrastructure manager** page where you can design your {{site.data.keyword.lakehouse_short}} by provisioning engines, services, buckets, and databases. You can also go to the **Query workspace** to create SQL queries to query your data.

The home page also shows alerts about your infrastructure and active queries.
