---

copyright:
  years: 2022, 2025
lastupdated: "2025-04-09"

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

# Performing semantic searches in {{site.data.keyword.lakehouse_short}}
{: #sal_search}

This topic provides users the steps to perform semantic searches on tables and views within {{site.data.keyword.lakehouse_full}} using natural language queries.

Following are some of the benefits of performing semantic search:

   * **Intuitive search**: Perform searches using natural language, eliminating the need for precise SQL syntax.
   * **Contextual understanding**: The system understands the context and meaning behind your search terms, providing more accurate results.
   * **Enhanced productivity**: Quickly locate relevant data with minimal effort, improving data discovery and analysis workflows.
   * **Unified search experience**: Search across multiple data tables and schemas seamlessly.

## Before you begin
{: #sal_searchbyb}

The semantic automation layer must be registered and enriched with data as instructed in the [Semantic automation for data enrichment](/docs/watsonxdata?topic=watsonxdata-sal_title) in {{site.data.keyword.lakehouse_short}}.

## Procedure
{: #sal_searchprcdre}

1. Log in to {{site.data.keyword.lakehouse_short}} console.
2. Navigate to **Browse data** tab of the **Data Manager**.

   Schemas and tables enriched with semantic metadata is visually indicated by an **AI** icon.
   {: note}

3. Locate the **Search AI enriched metadata** search bar within the **Browse data** window.
4. Perform semantic search by entering a natural language query into the search bar.

   The search provides a list of tables and views that match the requirement of the semantic search of your natural language query.

5. Click on a specific result to view its details, schema, and data.
