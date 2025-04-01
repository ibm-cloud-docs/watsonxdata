---

copyright:
  years: 2022, 2025
lastupdated: "2025-04-01"

keywords: watsonxdata, troubleshoot, optimizer

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

# Query Optimizer internal error updating statistics
{: #ts_optimizer_iceberg_stats}

## What’s happening
{: #ts_optimizer_iceberg_stats1}

The query rewrite procedure using **Query Optimizer** may fail when the statistics collected for an Iceberg table are invalid or inconsistent.

## Why it’s happening
{: #ts_optimizer_iceberg_stats2}

The rewrite procedure fails with the following error message:

   ```bash
   Internal error updating statistics in Db2 (see logs for details): The catalog statistic "<value>" for column "<volumn-name>" is out of range for its target column, has an invalid format, or is inconsistent in relation to some other statistic. Reason Code = "6".. SQLCODE=-1227, SQLSTATE=23521, DRIVER=4.33.32:
   ```
   {: screen}

## How to fix it
{: #ts_optimizer_iceberg_stats3}

1. Run the following command in Presto to obtain the actual cardinality of the Iceberg table:

   ```bash
   SELECT count(*)
   FROM <table-catalog>.<table-schema>.<table-name>;
   ```
   {: codeblock}

1. Use `ExecuteWxdQueryOptimizer` to execute the following SQL statement, which updates the card column in the sysstat.tables view with the actual cardinality obtained in step 1.

   ```bash
   ExecuteWxdQueryOptimizer 'update sysstat.tables set card=<value from count(*) in Presto> where TABSCHEMA='<table-catalog>.<table-schema>' AND TABNAME='<table-name>'';
   ```
   {: codeblock}

1. Run the procedure described in [Enhancing statistics for synced Iceberg tables](/docs/watsonxdata?topic=watsonxdata-optimizer_iceberg_stats) to successfully collect the enhanced statistics.
