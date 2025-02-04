---

copyright:
  years: 2022, 2024
lastupdated: "2025-01-26"

keywords: lakehouse, hms, {{site.data.keyword.lakehouse_short}}, hive, metastore

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

# Running queries from the Presto (C++) CLI or Query workspace
{: #exec_inspect_optimizer}

{{site.data.keyword.lakehouse_full}} allows running SQL queries from Presto (C++) CLI or through the **Query workspace** with or without using **Query Optimizer**.

## About this task
{: #optimizer_runqueryabt}

You can select the option of running Presto (C++) CLI queries with or without using **Query Optimizer** operator in {{site.data.keyword.lakehouse_short}} by using the following steps.

Running Presto (C++) queries:

1. Option 1: Running Presto (C++) queries by using **Query Optimizer**.

   a. Run the following command to enter into the directory `ibm-lh-client/bin`:
      ```bash
      cd ibm-lh-client/bin
      ```
      {: codeblock}

   b. Create an SQL file and export the file path to `LH_SANDBOX_DIR`. For example, with file name `sql-files`.
      ```bash
      export LH_SANDBOX_DIR=<path to sql-files>
      ```
      {: codeblock}

   c. Get the list of engine names and choose the one to be used. For example, engine name `engine1`.
      ```bash
      ./manage-engines --op=list
       export engine_name=engine1
      ```
      {: codeblock}

   d. Run the following command to run Presto (C++) queries using **Query Optimizer**.
      ```bash
      ./presto-run --engine=$engine_name --session enable_wxd_query_optimizer=true -f $LH_SANDBOX_DIR/sql-files.sql
      ```
      {: codeblock}

   You must use either fully qualified name (3 part name such as `<catalog.schema.table>`) or 2 part name with the USE statement to qualify the catalog and schema.

   Examples: 3 part name: `select * from "catalog".schema.table;`

   2 part name: `use "catalog".schema; followed by select * from schema.table;`

2. Option 2: Running Presto (C++) CLI queries without using **Query Optimizer**.

   a. Run the following command to enter into the directory ibm-lh-client/bin:
      ```bash
      cd ibm-lh-client/bin
      ```
      {: codeblock}

   b. Create an SQL file and export the file path to `LH_SANDBOX_DIR`. For example, with file name `sql-files`.

      ```bash
      export LH_SANDBOX_DIR=<path to sql-files>
      ```
      {: codeblock}

   c. Get the list of engine names and choose the one to be used. For example with engine name `engine1`.
      ```bash
      ./manage-engines --op=list
      export engine_name=engine1
      ```
      {: codeblock}

   d. Run the following command to run Presto (C++) queries using **Query Optimizer**.
      ```bash
      ./presto-run --engine=$engine_name --session enable_wxd_query_optimizer=false -f $LH_SANDBOX_DIR/sql-files.sql
      ```
      {: codeblock}

3. Follow the steps to get details of the queries and to verify if the queries executed are optimized:

   1. Log in to {{site.data.keyword.lakehouse_short}} console.

   2. From the navigation menu, open **Infrastructure manager** page.

   3. Click on the Presto (C++) engine to open the component details page.

   4. Copy and browse open the host URL of the Presto (C++) engine from the details page to open the **Cluster Overview** external web page.

   5. Enter the username and password to login to the **Cluster Overview** page.

      Username : The username is `ibmlhapikey` or `ibmlhapikey_<watsonx.datauser_id>`.
      Password : The API key of the {{site.data.keyword.lakehouse_short}} user. For more information about retrieving the API key, see [Generating the API key]({{site.data.keyword.ref-con-presto-serv-link}}).

   5. Click on the **Query ID** you want to verify. This will open the **Query Details** page.

   6. Open the JSON file from the **Query Details** page to verify the parameter `wxdQueryOptimized` value to be `true` or `false`. The optimized queries has the parameter value set to `true`.
