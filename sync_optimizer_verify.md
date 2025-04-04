---

copyright:
  years: 2022, 2025
lastupdated: "2025-03-24"

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

# Verifying table sync in {{site.data.keyword.lakehouse_short}}
{: #sync_optimizer_verify}

This topic provides details to verify that all expected tables have been successfully synced after the initial automatic as well as the manual sync operations in {{site.data.keyword.lakehouse_full}}.

## Before you begin
{: #sync_optimizer_verifybyb}

1. Install and activate **Query Optimizer** in {{site.data.keyword.lakehouse_short}}. See [Activating Query Optimizer Manager](/docs/watsonxdata?topic=watsonxdata-install_optimizer).
1. Names of catalogs and schemas for the tables being synced must be known.
1. The expected number of tables within each schema must be known.

## Procedure
{: #sync_optimizer_verifyprcdre}

1. Log in to {{site.data.keyword.lakehouse_short}} console.

1. Go to **Query workspace**.

1. Run the following command to retrieve a list of potential schema names:

   ```bash
   ExecuteWxdQueryOptimizer 'select distinct tabschema from syscat.tables where UPPER(tabschema) like '%SAMPLE_DATA%' ';
   ```
   {: codeblock}

1. Select the correct schema name (case-sensitive) from the results.

1. Run one of the following commands as needed:

   a. Run this command to count the number of tables within the specified schema:

      ```bash
      ExecuteWxdQueryOptimizer select count(1) from syscat.tables where tabschema = 'catalog.schema';
      ```
      {: codeblock}

      For example:

      ```bash
      ExecuteWxdQueryOptimizer select count(1) from syscat.tables where tabschema = 'sample_data.TPCDS_10GB';
      ```
      {: codeblock}

      Compare the result of this query with the expected number of tables. If the counts match, it indicates that all expected tables have been synced.

   b. Run this command to list all tables within the specified schema:

      ```bash
      ExecuteWxdQueryOptimizer 'select TABLEORG,TABSCHEMA,TABNAME from SYSCAT.TABLES where TABSCHEMA LIKE 'iceberg_data%'';
      ```
      {: codeblock}

1. Run the following query to check table statistics (such as cardinality):

   ```bash
   ExecuteWxdQueryOptimizer 'select tabname, card from syscat.tables where tabschema = 'catalog.schema' ';
   ```
   {: codeblock}

   For example:

      ```bash
      ExecuteWxdQueryOptimizer 'select tabname, card from syscat.tables where tabschema = 'sample_data.TPCDS_10GB';
      ```
      {: codeblock}

   The syscat views provide information about database objects. You can explore other system catalog views (example, syscat.columns, syscat.indexes) to verify other aspects of the synced tables as needed.
   {: note}
