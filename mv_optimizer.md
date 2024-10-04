---

copyright:
  years: 2022, 2024
lastupdated: "2024-10-04"

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

Materialized Views (MV) in {{site.data.keyword.lakehouse_full}} are pre-calculated results of complex queries. By storing these results, watsonx.data can significantly speed up query execution, especially for those involving joins and aggregations. Instead of re-running the original query each time, {{site.data.keyword.lakehouse_short}} can directly use the already computed Materialized View (MV) for faster query responses and improved overall performance.

Following are some of the benefits of Materialized Views (MV):

*. Improved query performance: Materialized View (MV) can significantly reduce query execution time by providing already computed results for frequently used complex queries.

*. Reduced resource consumption and expense: By avoiding repeated calculations, Materialized View (MV) can lower the workload on watsonx.data resources, leading to improved overall system efficiency and reduced cost.

*. Transparent Integration: Materialized View (MV) are seamlessly integrated into the query execution process, requiring minimal user intervention.

## Before you begin
{: #mv_optimizerbyb}

1. Install and activate Query Optimizer. For more information, see [Activating Query Optimizer](watsonxdata?topic=watsonxdata-install_optimizer).
2. Sync Query Optimizer with watsonx.data meta store. For more information, see [Manually syncing Query Optimizer](watsonxdata?topic=watsonxdata-sync_optimizer_meta).

## Procedure
{: #mv_optimizerprcdre}

Follow the steps to enable Materialized View (MV) feature for **Query Optimizer** in {{site.data.keyword.lakehouse_short}}.

1. Set the property for `enable-query-optimizer-materialized-view` to `true` to enable Materialized View (MV) feature at global level using patch API. See [patch API curl example](https://cloud.ibm.com/apidocs/watsonxdata-software#update-presto-engine).

   Example:

   ```bash
   curl --location --request PATCH 'https://us-south.lakehouse.dev.cloud.ibm.com/lakehouse/api/v2/prestissimo_engines/prismo965' \
   --header 'AuthInstanceId: crn:v1:staging:public:lakehouse:us-south:a/48ec9148b7d9409c9ee15c779bd5c7cc:2c27e276-e841-47ed-b61a-1dd14b4d3600::' \
   --header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJJQk1MSCIsInN1YiI6InNvd21peWFwazE1QGlibS5jb20iLCJhdWQiOlsiQU1TIl0sImV4cCI6MTcyNzE2NDE4NywiaWF0IjoxNzI3MTYyOTg3LCJ1aWQiOiJJQk1pZC02OTIwMDA5M1g3IiwicGVybWlzc2lvbnMiOlsibGFrZWhvdXNlLm1ldGFzdG9yZS5hZG1pbiIsImxha2Vob3VzZS5kYXNoYm9hcmQudmlldyIsImxha2Vob3VzZS51c2VydnBjLm1hbmFnZSJdLCJncm91cHMiOltdLCJpbnN0YW5jZSI6eyJ1c2VybmFtZSI6InNvd21peWFwazE1QGlibS5jb20iLCJpbnN0YW5jZV9uYW1lIjoiIiwiaW5zdGFuY2VfaWQiOiJjcm46djE6c3RhZ2luZzpwdWJsaWM6bGFrZWhvdXNlOnVzLXNvdXRoOmEvNDhlYzkxNDhiN2Q5NDA5YzllZTE1Yzc3OWJkNWM3Y2M6MmMyN2UyNzYtZTg0MS00N2VkLWI2MWEtMWRkMTRiNGQzNjAwOjoiLCJyb2xlcyI6WyJjcm46djE6Ymx1ZW1peDpwdWJsaWM6aWFtOjo6OnJvbGU6T3BlcmF0b3IiLCJjcm46djE6Ymx1ZW1peDpwdWJsaWM6aWFtOjo6OnJvbGU6Vmlld2VyIiwiY3JuOnYxOmJsdWVtaXg6cHVibGljOmlhbTo6Ojpyb2xlOkF1dGhvcml6YXRpb25EZWxlZ2F0b3IiLCJjcm46djE6Ymx1ZW1peDpwdWJsaWM6aWFtOjo6OnNlcnZpY2VSb2xlOlJlYWRlciIsImNybjp2MTpibHVlbWl4OnB1YmxpYzppYW06Ojo6c2VydmljZVJvbGU6TWFuYWdlciIsImNybjp2MTpibHVlbWl4OnB1YmxpYzppYW06Ojo6cm9sZTpBZG1pbmlzdHJhdG9yIiwiY3JuOnYxOmJsdWVtaXg6cHVibGljOmlhbTo6Ojpyb2xlOkVkaXRvciIsImNybjp2MTpibHVlbWl4OnB1YmxpYzppYW06Ojo6c2VydmljZVJvbGU6V3JpdGVyIl19LCJ1c2VybmFtZSI6InNvd21peWFwazE1QGlibS5jb20iLCJkaXNwbGF5X25hbWUiOiJTb3dtaXlhIFAgSyIsImNlcnRfc2VyaWFsX251bWJlciI6IjM2ODQzODgzNDEzMTU1MjE1MDk1Mjc4NjQ1MjU2OTk0NTk0MTA0NTE0NSIsImJzc19hY2NvdW50X2lkIjoiNDhlYzkxNDhiN2Q5NDA5YzllZTE1Yzc3OWJkNWM3Y2MifQ.tHLhbgfMxUXTs0k9qavUVAdUyDgSJqF1xLaPsdejMgv3eHOx0t9BPo97l4AXNEioE5IvnvXqxS1p4FnRnaDXyASJkzfB6C_rjaE8qTrH-MiquaupO77pkrfBKGrNsrDWksbyb4qmPaXFw_EBQt0hawyDyC1Lta9E5qnhDHF5_9is5llLQNyE6czsP1TJKKKVFadrX5G4acdPHvk0cfkLQNf-QCxZJu07agpt44zW8ajzx14K7BpvFZM5liVc_sdFgClk8OOdPYLSFhhg6nDGXV-4uHO-pJ4YdENU5ExFlTvR_155r5Pc9Wa-DwS4634Fq_rf2jiwWAn5BYACBu-GlQ' \
   --header 'Content-Type: application/json' \
   --data '{
       "description": "updated description for prestissimo engine",
       "engine_display_name": "sample",
       "engine_properties": {
           "configuration": {
               "coordinator": {},
               "worker": {}
           },
           "global": {"enable-query-optimizer-materialized-view":"true"}
       },
       "engine_restart": "force",
       "remove_engine_properties": {
           "configuration": {
               "coordinator": [],
               "worker": []
           },
           "catalog": {
               "hive_data": []
           },
           "jvm": {
               "coordinator": []
           },
           "velox": []
       },
       "tags": [
           "tag1",
           "tag2"
       ]
   }'
   ```
   {: codeblock}

3. Identify and select queries that are complex, frequently used, and involve joins or aggregations.

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

4. Run the following command to create the Materialized View (MV) named `mv` for the selected query.

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

5. Run the following command to analyze the Materialized View (MV) table mv.

   ```bash
   analyze mv;
   ```
   {: codeblock}

6. Run the following commands to synchronize the newly created Materialized View (MV) table `mv` with the Query Optimizer.

   1. Run the following command to register the Materialized View (MV) table `mv`:

   ```bash
   ExecuteWxdQueryOptimizer 'call syshadoop.external_catalog_sync('<catalog>', '<SCHEMA>', '<mvtablename>', 'REPLACE', 'CONTINUE', 'OAAS')';
   ```
   {: codeblock}

   2. Run the following command to add the Materialized View (MV) table `mv`:

   ```bash
   ExecuteWxdQueryOptimizer 'values (prestosqlddl('alter table <mvtablename> add materialized query (<query>) data initially deferred refresh deferred maintained by user enable query optimization', '<catalog>', '<SCHEMA>'))';
   ```
   {: codeblock}

   3. Run the following command to set the constraints for the Materialized View (MV) table `mv`:

   ```bash
   ExecuteWxdQueryOptimizer 'values (prestosqlddl('set constraints for <mvtablename> all immediate unchecked', '<catalog>', '<SCHEMA>'))';
   ```
   {: codeblock}

7. Set the use_materialized_views session variable to true to enable Materialized View (MV) for query optimization in a particular session:

   ```bash
   SET SESSION use_materialized_views=true;
   ```
   {: codeblock}
