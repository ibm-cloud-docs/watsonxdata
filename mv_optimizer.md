---

copyright:
  years: 2022, 2025
lastupdated: "2025-08-26"

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

# Optimizing queries using Materialized View (MV) in Query optimizer
{: #mv_optimizer}

Materialized Views (MV) in {{site.data.keyword.lakehouse_full}} are pre-calculated results of complex queries. By storing these results, {{site.data.keyword.lakehouse_short}} can significantly speed up query execution, especially for those involving joins and aggregations. Instead of re-running the original query each time, {{site.data.keyword.lakehouse_short}} can directly use the already computed Materialized View (MV) for faster query responses and improved overall performance.

Following are some of the benefits of Materialized Views (MV):

   * Improved query performance: Materialized View (MV) can significantly reduce query execution time by providing already computed results for frequently used complex queries.

   * Reduced resource consumption and expense: By avoiding repeated calculations, Materialized View (MV) can lower the workload on watsonx.data resources, leading to improved overall system efficiency and reduced cost.

   * Transparent Integration: Materialized View (MV) are seamlessly integrated into the query execution process, requiring minimal user intervention.

## Before you begin
{: #mv_optimizerbyb}

1. Install and activate Query Optimizer. For more information, see [Activating Query Optimizer](/docs/watsonxdata?topic=watsonxdata-install_optimizer).
2. Sync Query Optimizer with watsonx.data meta store. For more information, see [Manually syncing Query Optimizer](/docs/watsonxdata?topic=watsonxdata-sync_optimizer_meta).

## Procedure
{: #mv_optimizerprcdre}

Follow the steps to enable Materialized View (MV) feature for **Query Optimizer** in {{site.data.keyword.lakehouse_short}}.

1. Identify and select queries that are complex, frequently used, and involve joins or aggregations.

   For example, consider the following sample query as a potential Materialized View (MV) candidate:

   ```bash
   select sum(sales), region
   from (
     select sales, region from customer_sales
     union all
     select sales, region from store_sales
     union all
     select sales, region from union_sales
     union all
     select sales, region from online_sales
   ) group by region;
   ```
   {: codeblock}

3. Run the following command to create the Materialized View (MV) named `mv` for the selected query.

   ```bash
   create table mv (sumsales, region) as (
     select sum(sales),  region
     from (
       select sales, region from customer_sales
       union all
       select sales, region from store_sales
       union all
       select sales, region from union_sales
       union all
       select sales, region from online_sales
     ) group by region
   );
   ```
   {: codeblock}

   Auto refresh of Materialized View (MV) table is not available yet. To update an existing table, you must delete the table and create the Materialized View (MV) again.
   {: note}

4. Run the following command to analyze the Materialized View (MV) table mv.

   ```bash
   analyze mv;
   ```
   {: codeblock}

5. Run the following commands to synchronize the newly created Materialized View (MV) table `mv` with the Query Optimizer.

   1. Run the following command to synchronize the Materialized View table `mv` from {{site.data.keyword.lakehouse_short}} to Db2:

   ```bash
   ExecuteWxdQueryOptimizer 'call syshadoop.external_catalog_sync('<catalog>', '<SCHEMA>', '<mvtablename>', 'REPLACE', 'CONTINUE', 'OAAS')';
   ```
   {: codeblock}

   2. Run the following command to synchronize statistics of Materialized View table `mv` in Db2:

   ```bash
   ExecuteWxdQueryOptimizer 'call ext_metastore_stats_sync('<catalog>', '<SCHEMA>', '<MVTABLENAME>', '<engine-internal-URL:port>', '<admin>', '<admin-password>', 'true')';
   ```
   {: codeblock}

   3. Run the following command to add the Materialized View (MV) table `mv` in Db2:

   ```bash
   ExecuteWxdQueryOptimizer 'values (prestosqlddl('alter table <mvtablename> add materialized query (<query>) data initially deferred refresh deferred maintained by user enable query optimization', '<catalog>', '<SCHEMA>'))';
   ```
   {: codeblock}

   4. Run the following command to set the constraints for the Materialized View (MV) table `mv`:

   ```bash
   ExecuteWxdQueryOptimizer 'values (prestosqlddl('set constraints for <mvtablename> all immediate unchecked', '<catalog>', '<SCHEMA>'))';
   ```
   {: codeblock}

6. Set the use_materialized_views session variable to true to enable Materialized View (MV) for query optimization in a particular session:

   ```bash
   SET SESSION use_materialized_views=true;
   ```
   {: codeblock}

7. Run SQL queries to leverage Materialized view tables for query optimization after enabling and configuring them.
