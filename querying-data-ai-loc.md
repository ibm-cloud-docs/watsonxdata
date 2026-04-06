---

copyright:
  years: 2022, 2025
lastupdated: "2026-04-06"

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

# Installing and configuring the local MCP server
{: #querying-data-ai-loc}

You must install and configure the local MCP server on your local computer.

## System requirements
{: #querying-loc-1}

**Software prerequisites**
{: #querying-loc-2}

Before you begin, ensure that your system meets the following requirements:

| Component | Requirement | Notes |
|-----------|-------------|-------|
| Python | Version 3.11 or later | [Download Python](https://www.python.org/downloads/) |
| Package manager | uv | [Install uv](https://github.com/astral-sh/uv) |
| IBM Cloud account | Active account | [Register for IBM Cloud](https://cloud.ibm.com/registration) |
{: caption="System requirements" caption-side="bottom"}

**IBM {{site.data.keyword.lakehouse_short}} requirements**
{: #querying-loc-3}

You must have access to the following IBM {{site.data.keyword.lakehouse_short}} resources:

- **{{site.data.keyword.lakehouse_short}} instance**: A provisioned and running instance

   - [Provision a lite plan instance](/docs/watsonxdata?topic=watsonxdata-tutorial_prov_lite_1) or [Provision an enterprice plan instance](/docs/watsonxdata?topic=watsonxdata-getting-started_1)

   - [Set up {{site.data.keyword.lakehouse_short}} lite plan](/docs/watsonxdata?topic=watsonxdata-tutorial_hp_intro)

- **IBM Cloud API key**: An API key with appropriate permissions

   - [Create an API key](https://cloud.ibm.com/iam/apikeys)

**Required configuration information**
{: #querying-loc-4}

Collect the following information before installation:

- **Base URL**: The URL of your {{site.data.keyword.lakehouse_short}} instance
   - Format: `"https://your-instance.lakehouse.cloud.ibm.com/lakehouse/api/lakehouse/api`

- **Instance CRN**: The Cloud Resource Name of your instance. To find CRN, refer [Getting connection information](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-get_connection).

   - Format: `crn:v1:bluemix:public:lakehouse:us-south/a/...`

   - To locate your Instance CRN:

    1. Log in to the {{site.data.keyword.lakehouse_short}} console.
    2. On the **Instance details** or **Configuration** page, locate the **CRN** field in the details section.
    3. Click the copy icon next to the CRN to copy it to your clipboard.

- **IAM API Key**: Your IBM Cloud API key with {{site.data.keyword.lakehouse_short}} access permissions.

## Installing the MCP Server
{: #querying-loc-5}

You can install the IBM {{site.data.keyword.lakehouse_short}} MCP Server using one of the following methods:

### Installing with pipx
{: #querying-loc-6}

1. Run the following code to install pipx if not already installed.

   ```bash
   pip install pipx
   ```
   {: codeblock}

2. Run the following code to install the MCP server.

   ```bash
   pipx install ibm-watsonxdata-mcp-server
   ```
   {: codeblock}


### Installing with pip
{: #querying-loc-7}

Use this method if you prefer to install the server in your user Python environment.

1. Run the following code to install the MCP server.

   ```bash
   pip install --user ibm-watsonxdata-mcp-server
   ```
   {: codeblock}

To install MCP sever for development setup, refer [IBM {{site.data.keyword.lakehouse_short}} MCP Server](https://github.com/IBM/ibm-watsonxdata-mcp-server?tab=readme-ov-file).

## Configuring the MCP server
{: #querying-loc-8}

After installation, configure your agents to communicate with the MCP server.

### Find the MCP server executable
{: #querying-loc-9}

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

### Connect your Agents with MCP Server
{: #querying-loc-10}

After locating the MCP server executable, configure your agents to connect to the server. See the following topics for specific instructions:

- [Configuring Claude Desktop](/docs/watsonxdata?topic=watsonxdata-configuring-claude)
- [Configuring IBM Bob](/docs/watsonxdata?topic=watsonxdata-configuring-bob)

### Querying data with the MCP tool
{: #querying-loc-11}

After configuration with AI agents, you can interact with your {{site.data.keyword.lakehouse_short}} instance through natural language conversations with your agent. For more information, see [Querying data with the MCP tool](/docs/watsonxdata?topic=watsonxdata-working_with_MCP_server).
