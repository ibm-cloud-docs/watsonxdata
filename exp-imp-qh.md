---

copyright:
  years: 2022, 2025
lastupdated: "2025-12-15"

keywords: lakehouse, exporting, importing, query history, watsonx.data

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

# Exporting and importing the query history
{: #eximp-q-hist}

The Presto coordinator stores the query history in `system.runtime.queries` table. But `system.runtime.queries` table truncates when you restart Presto, resulting in loss of query history.
To mitigate this issue, you can export query history as a csv file and also import the query history from the system.runtime.queries table to a non-system table.
{: shortdesc}

It is recommended to periodically export the query history to avoid losing it.

To import and export the query history, you must install the Presto CLI. For more information, see [Connecting to Presto server]({{site.data.keyword.ref-con-presto-serv-link}}){: external}.

Starting with {{site.data.keyword.lakehouse_short}} version 2.2.0, authentication using `ibmlhapikey` and `ibmlhtoken` as usernames is deprecated. These formats are phased out in 2.3.0 release. To ensure compatibility with upcoming versions, use the new format:`ibmlhapikey_<username>` and `ibmlhtoken_<username>`.
{: important}

## Exporting query history
{: #export-qh}

To export the query history, run the following command.

```bash
export PRESTO_PASSWORD=<your api_key>
```
{: codeblock}


```bash
./presto --server https://<port:host> --catalog system \
--schemaruntime --execute "select * from queries" \
--user ibmlhapikey --output-format CSV_HEADER > history.csv --password
```
{: codeblock}

This command generates a CSV file, which contains exported query history.

- **Example**

```bash
./presto --server https://8dac613f-ba5b-4c3c-8c96-
ce8de101f7cf.cdc406pd09pasng7elgg.databases.appdomain.cloud:30929 \
--execute "select * from system.runtime.queries" --output-format CSV_HEADER \
--user ibmlhapikey output-format CSV > history.csv --password
```
{: codeblock}

## Importing query history
{: #import-qh}

1. To import the query history, create a schema in a catalog in which you have the write access.

    ```bash
    create schema <non-system-catalog.schema-name> with (location=' s3a://<bucket-name>/<schema-name>')
    ```
    {: codeblock}

    - **Example**

    ```bash
    ./presto --server https://8dac613f-ba5b-4c3c-8c96-\
    ce8de101f7cf.cdc406pd09pasng7elgg.databases.appdomain.cloud:30929 \
    --execute "create schema hive_data.query_history with \
    (location='s3a://8dac613f-ba5b-4c3c-8c96-ce8de101f7cf-customer/query_history')" \
    --user ibmlhapikey --password
    ```
    {: codeblock}

2. Create a table in same catalog.

    This table must have same metadata as that of `system.runtime.queries` table. Use `CREATE TABLE AS SELECT` statement to create this table.
    {: note}

    ```bash
    create table <non-system-table-name> as select * from system.runtime.queries where 1=0;
    ```
    {: codeblock}

    `where 1=0` condition make sure that no rows are selected from a table, resulting in an empty result set.

    - **Example**

    ```bash
    ./presto --server https://8dac613f-ba5b-4c3c-8c96-ce8de101f7cf.cdc406pd09pasng7elgg.databases.appdomain.cloud:30929
    --execute "create table hive_data.query_history.queries as select * from system.runtime.queries where 1=0"
    --user ibmlhapikey --password
    ```
    {: codeblock}

3. To import the query history into the table that you have just created table, run the following query periodically.

    ```bash
    INSERT INTO <non-system-table-name>
    SELECT *
    FROM system.runtime.queries
    WHERE query_id NOT IN (SELECT query_id FROM <non-system-table-name>);
    ```
    {: codeblock}

    - **Example**

    ```bash
    ./presto --server \
    https://8dac613f-ba5b-4c3c-8c96-ce8de101f7cf.cdc406pd09pasng7elgg.databases.appdomain.cloud:3092 \
    –-execute "insert into hive_data.query_history.queries select * from system. runtime.queries \
    where query_id not in (select query_id from hive_data.query_history.queries)"
    --user ibmlhapikey --password
    ```
    {: codeblock}

4. To retrieve query history from both tables, use following statement.

    ```bash
    select * from <non-system-table-name> union select * from `system.runtime.queries` order by created;
    ```
    {: codeblock}

    - **Example**

    ```bash
    ./presto --server \
    https://23b06b14-342b-4ed2-841d-7f02ca9ae788.cdc406pd09pasng7elgg.databases.appdomain.cloud:31530 \
    --execute " select * from hive_data.query_history.queries union \
    select * from system.runtime.queries order by created " \
    --output-format=CSV_HEADER --user ibmlhapikey --password
    ```
    {: codeblock}
