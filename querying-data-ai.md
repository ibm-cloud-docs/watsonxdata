---

copyright:
  years: 2022, 2025
lastupdated: "2026-05-05"

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

# Interacting with data through an MCP server
{: #querying-data-ai}

You can securely access and explore your lakehouse data and metadata through natural language by using {{site.data.keyword.lakehouse_short}} Model Context Protocol (MCP) server and your AI agent.

The IBM {{site.data.keyword.lakehouse_short}} MCP Server is designed for the following users:

- AI agent developers who are building data-aware assistants
- Platform teams who are enabling governed AI access to lakehouse data
- Users who want conversational querying without exposing write access

## Connection models
{: #querying-data-ai-cm}

You can choose between a remote or a local MCP server. Both types provide the same tools and capabilities. 

Remote MCP server

: A fully managed endpoint that is hosted on IBM Cloud.

Local MCP server

: A locally installed server that runs on your local system.

The following table compares the characteristics of the remote and local MCP server implementations.

| Characteristic | Remote MCP server | Local MCP server |
|----------------|-------------------|------------------|
| Installation and resource requirements | None. Maintained by IBM. | Local installation and resource access required. |
| Intended use | Managed, scalable, and governed access | Highly customizable, environment-specific |
| Connectivity environment | Internet connection required. | Internet connection required. |
| Supported hosts | Any MCP-compliant host | Any MCP-compliant host |
| Integration and customization | Standardized integration | Custom integration |
{: caption="Characteristics of remote and local MCP servers" caption-side="bottom"}

## Capabilities
{: #squerying-data-ai-ft}

Both remote and local MCP servers provide the same capabilities. The IBM {{site.data.keyword.lakehouse_short}} MCP Server provides the following capabilities:

Query execution

: Execute SQL queries against your lakehouse data by using natural language.

Catalog operations

: Browse, search, and retrieve metadata from your data catalog.

Data ingestion

: Load and manage data into your watsonx.data instance.

Engine management

: Monitor and interact with your query engines.

Data security

: Secure your data through IBM Cloud Identity and Access Management (IAM) authentication with automatic token refresh. Write access is controlled to allow `INSERT` and `UPDATE` operations while restricting `DELETE` operations.

For the complete list of available tools and detailed use cases, refer [https://github.com/IBM/ibm-watsonxdata-mcp-server/blob/main/TOOLS.md](https://github.com/IBM/ibm-watsonxdata-mcp-server/blob/main/TOOLS.md){: external}.

## AI agent integrations
{: #squerying-data-ai-aiag}

You can use the IBM {{site.data.keyword.lakehouse_short}} MCP server with the following widely adopted MCP hosts:

   - IBM Bob
   - Claude Desktop
   - Other MCP-compatible clients. Any client that supports the MCP protocol can connect to the remote server

## MCP server architecture
{: #squerying-data-ai-ar}

The following diagram illustrates the process of querying data through the remote MCP server:

![architecture diagram](images/remote-mcp-architecture-diagram.svg){: caption="Remote MCP architecture diagram" caption-side="bottom"}{: width="1500px"}

The following diagram illustrates the process of querying data through the local MCP server.

![architecture diagram](images/mcp-query-execution-flow.svg){: caption="Local MCP architecture diagram" caption-side="bottom"}{: width="1500px"}

The MCP server enables conversational data access through the following workflow:

1. You submit a natural language query to your agent.
2. The agent interprets your request and determines the appropriate action.
3. The agent communicates with the MCP server, which then forwards the request to your {{site.data.keyword.lakehouse_short}} instance.
4. {{site.data.keyword.lakehouse_short}} processes the request and returns results to the MCP server.
5. The agent presents the results in a conversational format.

## Next steps
{: #querying-data-ai-nxt}

- [Remote MCP server setup](/docs/watsonxdata?topic=watsonxdata-remote-querying-data-ai-end){: external}
- [Local MCP server setup](/docs/watsonxdata?topic=watsonxdata-querying-data-ai-loc){: external}
