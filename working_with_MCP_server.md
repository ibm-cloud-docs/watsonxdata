---

copyright:
  years: 2022, 2025
lastupdated: "2026-03-05"

keywords: lakehouse, bucket, catalog, watsonx.data

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


# Querying data with the MCP tool
{: #working_with_MCP_server}

After configuration with AI agents, you can interact with your {{site.data.keyword.lakehouse_short}} instance through natural language conversations with your agent.

## Verifying connectivity
{: #working_with_MCP_server-vc}

Verify that the MCP server can successfully connect to your {{site.data.keyword.lakehouse_short}} instance.

**Procedure:**

1. Open your configured agent (Claude Desktop or IBM Bob).

2. Submit the following query:

   ```bash
   What is my watsonx.data instance status?
   ```
   {: codeblock}

**Expected result:** The agent returns information about your instance, including version, status, and available engines.

## Exploring available data
{: #working_with_MCP_server-ead}

Discover the schemas and tables available in your {{site.data.keyword.lakehouse_short}} instance.

**Procedure:**

1. To list available schemas:

   ```bash
   What schemas are available in my watsonx.data instance?
   ```
   {: codeblock}

2. To explore a specific schema:

   ```bash
   What tables exist in the tpch catalog?
   ```
   {: codeblock}

**Expected result:** The agent returns a list of available schemas or tables.

## Examining table structures
{: #working_with_MCP_server-ets}

View the structure and metadata of a specific table.

**Procedure:**

1. Submit a query in the following format:

   ```

   Describe the [table_name] table in [schema_name]
   ```
   {: codeblock}

   **Example:**

   ```bash
   Describe the customer table in tpch.tiny
   ```

**Expected result:** The agent returns column names, data types, and table properties.

## Querying data
{: #working_with_MCP_server-qd}

Execute SQL SELECT queries to retrieve data from your lakehouse.

Only `SELECT` queries are permitted. Attempts to execute `INSERT`, `UPDATE`, `DELETE`, or other data modification statements will be rejected.
{: note}


**Procedure:**

Submit queries using either natural language or SQL syntax:

- Natural language example:

   ```bash
   Show me the top 10 customers by account balance
   ```

- SQL syntax example:

   ```bash
   SELECT * FROM tpch.tiny.customer LIMIT 10
   ```

**Expected result:** The agent executes the query and presents results in a formatted table.
