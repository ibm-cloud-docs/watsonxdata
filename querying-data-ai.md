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

# Querying data through agents by using the MCP server
{: #squerying-data-ai}

The IBM {{site.data.keyword.lakehouse_short}} Model Context Protocol (MCP) Server enables agents to interact with IBM {{site.data.keyword.lakehouse_short}} lakehouse instances through natural language interfaces. You can use this server to securely access and explore your lakehouse data and metadata through the Model Context Protocol, with built-in read-only protection to ensure data integrity.

The IBM {{site.data.keyword.lakehouse_short}} MCP Server is designed for the following users:

- AI agent developers who are building data-aware assistants
- Platform teams who are enabling governed AI access to lakehouse data
- Users who want conversational querying without exposing write access

## Capabilities
{: #squerying-data-ai-ft}

The IBM {{site.data.keyword.lakehouse_short}} MCP Server provides the following capabilities:

**Data access and exploration**
{: #squerying-data-ai-dt}

- Execute SQL SELECT queries using natural language or direct SQL syntax
- Browse data catalogs and schemas
- Inspect table structures and metadata, including columns, data types, properties, partitioning, and primary keys
- Monitor engine status and availability

**Data security**
{: #squerying-data-ai-se}

- Read-only access enforcement (SELECT queries only)
- IBM Cloud Identity and Access Management (IAM) authentication
- Automatic token refresh mechanism
- Query validation and safety checks before execution
- Potentially unsafe operations are blocked

**Transport mechanisms**
{: #squerying-data-ai-trm}

- stdio transport for local subprocess communication. For implementation guidelines and security best practices, refer [MCP Transports Specification](https://modelcontextprotocol.io/specification/2025-11-25/basic/transports).

**AI agent integrations**
{: #squerying-data-ai-aiag}

- Integrates with the following AI agents on your local computer:

   - IBM Bob
   - Claude Desktop

## Configuration workflow
{: #squerying-data-ai-cfwr}

To configure the MCP server, complete these main tasks:

1. Install and configure the MCP server on your local computer. See Installing and configuring the MCP server for querying data.
2. Configure your AI agent to work with the MCP server and connect to {{site.data.keyword.lakehouse_short}}. See [Configuring IBM Bob](/docs/watsonxdata?topic=watsonxdata-configuring-bob) or [Configuring Claude Desktop](/docs/watsonxdata?topic=watsonxdata-configuring-claude).

## Understanding the interaction model
{: #working_with_MCP_server-uim}

The MCP server enables conversational data access through the following workflow:

1. You submit a natural language query to your agent
2. The agent interprets your request and selects the appropriate MCP tool
3. The MCP server executes the operation against your {{site.data.keyword.lakehouse_short}} instance
4. Results are returned to the agent
5. The agent presents the results in a conversational format


## MCP server architecture
{: #squerying-data-ai-ar}

The following diagram illustrates the process of querying data through the MCP server.

![architecture diagram](images/mcp-query-execution-flow.svg){: caption="Architecture diagram" caption-side="bottom"}{: width="1500px"}

The MCP server enables conversational data access through the following workflow:

1. You submit a natural language query to your agent.
2. The agent interprets your request and selects the appropriate MCP tool.
3. The MCP server executes the operation against your watsonx.data instance.
4. Results are returned to the agent.
5. The agent presents the results in a conversational format.
