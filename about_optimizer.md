---

copyright:
  years: 2022, 2024
lastupdated: "2024-09-23"

keywords: lakehouse, **Query Optimizer**, {{site.data.keyword.lakehouse_short}}

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

# Query Optimizer
{: #about_optimizer}

In the domain of database management systems, query optimizers play a pivotal role in ensuring efficient execution of database queries. **Query Optimizer**, a component of {{site.data.keyword.lakehouse_full}}, improves the performance of queries that are processed by Presto (C++) engine. If optimization is analyzed to be feasible, the query undergoes rewriting; otherwise, the native engine optimization takes precedence.

**Query Optimizer** is not supported for Presto (Java).
{: note}

Within {{site.data.keyword.lakehouse_short}}, **Query Optimizer** operates as a component, tasked with optimizing queries. It accepts a standard SQL query as input and generates an optimized SQL equivalent, which is tailored for enhanced execution by Presto (C++). In instances where optimization is not feasible, the system reverts to using the original query.

**Query Optimizer** emerges as a valuable addition to the {{site.data.keyword.lakehouse_short}}, empowering users to optimize their queries and achieve enhanced performance from their engines.

You can see [Activating Query Optimizer Manager](watsonxdata?topic=watsonxdata-install_optimizer) section for more information.

## Advantages of **Query Optimizer**
{: #queryopti_advantage}

The query optimization feature of Db2 is leveraged in {{site.data.keyword.lakehouse_short}} and the key factors considered include:

* {{site.data.keyword.lakehouse_short}} uses Db2 as the Decades-Honed Query Optimization for Peak Performance.

   Leveraging extensive development, query optimization feature of Db2 analyzes your SQL queries and generates optimal execution plans. Key factors considered include:
   * Accurate statistics: RUNSTATS gathers data distribution and cardinality estimates for informed decisions.
   * Well-designed indexes and constraints: These guide the optimizer towards efficient access paths and enforce data integrity.
   * Advanced techniques for complex queries: Cost-based optimization and cardinality estimation ensure efficient processing.

* Enhanced Query Performance: **Query Optimizer** effectively optimizes queries, leading to significant performance improvements.
* Seamless Integration: **Query Optimizer** seamlessly integrates with existing {{site.data.keyword.lakehouse_short}} infrastructure, ensuring a smooth adoption process.
* Flexible Optimization: **Query Optimizer** operates flexibly as users can enable and disable the feature either at global or session level.
* * **Query Optimizer** supports Hive and Iceberg tables.

## Limitation of **Query Optimizer**
{: #queryopti_limits}

* **Query Optimizer** only support Presto C++.
* When metastores are synced, all schemas and tables are in the uppercase. For example, `"catalog".SCHEMA.TABLE`.
* Three-part name queries need quotation marks around the catalog name in lowercase (`"catalog".SCHEMA.TABLE`). Query returns an error otherwise.
* For optimal performance, you must define constraints like NOT NULL, Primary key, and Foreign key in `Query Optimizer engine` after the tables are synced.
* Upon enabling the **Query Optimizer**, metadata for all catalogs currently connected to any Presto engine will be automatically synchronized with the optimizer engine. However, subsequent additions of catalogs or schemas after enabling the optimizer will require manual metadata synchronization by the user. Refer to [Syncing Query Optimizer](watsonxdata?topic=watsonxdata-sync_optimizer_meta) for detailed instructions.
* If a catalog or schema was inaccessible or corrupted during **Query Optimizer** deployment, its metadata will be absent in the optimizer engine. To ensure all objects are present as expected, users should utilize the commands outlined on [Syncing Query Optimizer](watsonxdata?topic=watsonxdata-sync_optimizer_meta) to manually validate and potentially synchronize missing metadata.
* **Query Optimizer** functionality is dependent on the presence of at least one active Presto C++ engine within your Watsonx.data instance. Attempting to remove the last remaining Presto C++ engine while **Query Optimizer** is enabled will trigger a deactivation of the **Query Optimizer** itself. A confirmation prompt will be presented within the user interface to prevent accidental deactivation.
* **Query Optimizer** do not support views.
* Decimal and float columns in the projection list might interchange and can cause mismatch in data type.
* Certain queries (full outer join, anti join) do not return the correct result.
* Special characters in the identifier do not work properly.
* Interval is not supported. Use date_add.
