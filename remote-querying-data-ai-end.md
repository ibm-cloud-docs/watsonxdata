---

copyright:
  years: 2022, 2025
lastupdated: "2026-03-31"

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

# Obtain the endpoint for the remote MCP server
{: #remote-querying-data-ai-end}

To connect your AI agent with {{site.data.keyword.lakehouse_short}} tools, you must obtain the endpoint for the remote MCP server.

## Prerequisites
{: #remote-querying-data-ai-en-pre}

Before connecting to the Remote MCP Server, ensure you have:

- **{{site.data.keyword.lakehouse_short}} instance** - A provisioned and running instance

   - [Provision a lite plan instance](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-tutorial_prov_lite_1) and [Provision an enterprice plan instance](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-getting-started_1)

   - [Set up {{site.data.keyword.lakehouse_short}} lite plan](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-tutorial_hp_intro)

- **IBM Cloud API key** - An API key with appropriate permissions to access your {{site.data.keyword.lakehouse_short}} instance. To create IBM Cloud API key, see [Creating an API key](https://cloud.ibm.com/docs/account?topic=account-userapikey&interface=ui#create_user_key).

- **Instance CRN**: The Cloud Resource Name of your instance. To find CRN, refer [Getting connection information](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-get_connection).

   - Format: `crn:v1:bluemix:public:lakehouse:us-south/a/...`

   - To locate your Instance CRN:

    1. Log in to the {{site.data.keyword.lakehouse_short}} console.
    2. On the **Instance details** or **Configuration** page, locate the **CRN** field in the details section.
    3. Click the copy icon next to the CRN to copy it to your clipboard.

- **MCP-compatible client** - An AI assistant or application that supports the Model Context Protocol (Claude Desktop, or IBM Bob)

## Remote MCP server endpoint
{: #remote-querying-data-ai-rmcp}

To connect to the remote MCP server, use the following endpoint:

`https://<your-instance-url>/api/v1/mcp/watsonxdata`

Replace `<your-instance-url>` with the URL of your specific {{ site.data.keyword.wxdata }} instance.

### Connect your Agents with remote MCP Server
{: #remote-querying-data-ai-cng}

After connecting the remote MCP server, configure your agents to connect to the server. See the following topics for specific instructions:

- [Configuring Claude Desktop](/docs/watsonxdata?topic=watsonxdata-configuring-claude)
- [Configuring IBM Bob](/docs/watsonxdata?topic=watsonxdata-configuring-bob)

### Querying data with the MCP tool
{: #remote-querying-data-ai-qdw}

After configuration with AI agents, you can interact with your {{site.data.keyword.lakehouse_short}} instance through natural language conversations with your agent. For more information, see [Querying data with the MCP tool](/docs/watsonxdata?topic=watsonxdata-working_with_MCP_server).
