---

copyright:
  years: 2022, 2025
lastupdated: "2026-03-04"

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


# Configuring the MCP server
{: #squerying-data-ai-cnf}

After installation, configure your agents to communicate with the MCP server.

## Find the MCP server executable
{: #squerying-data-ai-srv}

Complete the steps below to locate the MCP server executable based on your operating system. You will use this path when configuring your agents.

- **macOS or Linux**

   Open a terminal and run:

   ```bash
   which ibm-watsonxdata-mcp-server
   ```
   {: codeblock}

- **Windows (PowerShell)**

   Open PowerShell and run:

   ```bash
   where.exe ibm-watsonxdata-mcp-server
   ```
   {: codeblock}

## Connect your Agents with MCP Server
{: #squerying-data-ai-caw}

After locating the MCP server executable, configure your agents to connect to the server. See the following topics for specific instructions:

- [Configuring Claude Desktop](/docs/watsonxdata?topic=watsonxdata-configuring-claude)
- [Configuring IBM Bob](/docs/watsonxdata?topic=watsonxdata-configuring-bob)

## Working with the MCP Tool
{: #squerying-data-ai-wrkm}

The following topic provides detailed guidance on using the MCP server tools to interact with your {{site.data.keyword.lakehouse_short}} instance.

- [Working with the MCP Tool](/docs/watsonxdata?topic=watsonxdata-working_with_MCP_server)
