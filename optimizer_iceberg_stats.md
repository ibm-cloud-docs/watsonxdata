---

copyright:
  years: 2022, 2025
lastupdated: "2025-08-27"

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

# Enhancing statistics for synced Iceberg tables
{: #optimizer_iceberg_stats}

This topic gives the details to gather enhanced statistics for Iceberg tables that are synchronized with the {{site.data.keyword.lakehouse_full}} metastore. It uses the `EXT_METASTORE_STATS_SYNC` stored procedure to collect and update statistical information within the metastore, which can improve the performance of query optimization and execution.

## Before you begin
{: #optimizer_iceberg_statsbyb}

1. Make sure that the manual synchronization procedure between the **Query Optimizer** and the {{site.data.keyword.lakehouse_short}} metastore is completed successfully if needed. See [Manually syncing Query Optimizer with Watsonx.data metastore](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-sync_optimizer_meta).

   The instructions in this topic can now be executed using the enhanced feature [Managing statistical updates from the Optimizer dashboard](/docs/watsonxdata?topic=watsonxdata-analyze_optimizer), which enables advanced query performance enhancements and optimization capabilities across multiple
   catalogs.
   {: note}

## Procedure
{: #optimizer_iceberg_statsprcdre}

1. Run the following command to get enhanced statistics for an Iceberg table that is synced:

   ```bash
   ExecuteWxdQueryOptimizer 'CALL EXT_METASTORE_STATS_SYNC(
     '<CATALOG_NAME>',
     '<SCHEMA_NAME>',
     '<TABLE_NAME>',
     '<PRESTO_INTERNAL_HOST>',
     '<PRESTO_USER>',
     '<PRESTO_PWD>',
     'true'
   )';
   ```
   {: codeblock}

   `<CATALOG_NAME>`: The name of catalog (case-sensitive).

   `<SCHEMA_NAME>`: The name of schema in uppercase.

   `<TABLE_NAME>`: The name of table in uppercase. It is recommended to gather statistics for each table individually.

   `<PRESTO_INTERNAL_HOST>`: The internal hostname of Presto engine of which the statistics is collected from. You can find the connection details of Presto engine by clicking on the engine in the Infrastructure manager page of {{site.data.keyword.lakehouse_short}}.

   `<PRESTO_USER>`: The Presto username that is used to run the statistics collection. Username can be `ibmlhapikey` or `ibmlhtoken`. It is recommended to use `ibmlhapikey`.

   `<PRESTO_PWD>`: The Presto password that is used to run the statistics collection. Password can be a base64 API key or token corresponding to the username.

   Verify the sync operation in a few minutes by following the procedure in [Verifying table sync in watsonx.data](/docs/watsonxdata?topic=watsonxdata-sync_optimizer_verify).
   {: note}
