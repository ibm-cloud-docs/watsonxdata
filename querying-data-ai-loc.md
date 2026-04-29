---

copyright:
  years: 2022, 2025
lastupdated: "2026-04-29"

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

# Setting up a local MCP server
{: #querying-data-ai-loc}

You must install and configure the local MCP server on your local computer.

## Prerequisite software
{: #querying-loc-1}

Before you begin, ensure that your system meets the following requirements:

| Component | Requirement | Notes |
|-----------|-------------|-------|
| Python | Version 3.11 or later | [Download Python](https://www.python.org/downloads/){: external} |
| Package manager | uv | [Install uv](https://github.com/astral-sh/uv){: external} |
{: caption="System requirements" caption-side="bottom"}

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

To install MCP sever for development setup, refer [IBM {{site.data.keyword.lakehouse_short}} MCP Server](https://github.com/IBM/ibm-watsonxdata-mcp-server?tab=readme-ov-file){: external}.

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

## Getting the required configuration information
{: #querying-loc-10}

You need to provide values for the following variables in the agent configuration file:

- `path/to/ibm-watsonxdata-mcp-server`: The MCP server executable location
- `WATSONX_DATA_BASE_URL`: The `<console-host>` portion of your {{site.data.keyword.lakehouse_short}} instance URL for the MCP server endpoint. The MCP server endpoint has the following format:
   - `https://<console-host>/lakehouse/api`
- `WATSONX_DATA_API_KEY`: Your IBM Cloud API key
- `WATSONX_DATA_INSTANCE_ID`: The Cloud Resource Name (CRN) of {{site.data.keyword.lakehouse_short}} instance

To get the required information:

1. To get the MCP server executable location, open a terminal and run the appropriate command:

   - **macOS or Linux**

     1. Open a terminal and run:

        ```bash
        which ibm-watsonxdata-mcp-server
        ```
        {: codeblock}

   - **Windows (PowerShell)**

      1. Open PowerShell and run:

        ```bash
        where.exe ibm-watsonxdata-mcp-server
        ```
        {: codeblock}

2. Log into IBM Cloud.
3. To find the `<console-host>` and CRN values, go to **Resources** and select your {{site.data.keyword.lakehouse_short}} instance.
4. Get the value of `<console-host>` by copying the first part of the web console URL. For example: `console-ibm-cator.lakehouse.saas.ibm.com`
5. Get your {{site.data.keyword.lakehouse_short}} instance CRN by copying the CRN value. The CRN has the following format: `crn:v1:bluemix:public:lakehouse:us-south/a/...`
6. Copy your IBM Cloud API key or if necessary, create one. See [Creating an API key](https://cloud.ibm.com/docs/account?topic=account-userapikey&interface=ui#create_user_key){: external}.

## Configuring the agent
{: #querying-loc-11}

You must configure the agent to connect to the MCP server by editing the agent configuration file:

- The IBM Bob configuration file is (file path).

    ```bash
     ~/Library/Application Support/Bob-IDE/User/globalStorage/ibm.bob-code/settings/mcp_settings.json
    ```

- The Claude Desktop configuration file location varies by operating system:

    | Operating System | Configuration File Path |
    |-----------------|-------------------------|
    | macOS | `~/Library/Application Support/Claude/claude_desktop_config.json` |
    | Windows | `%APPDATA%\Claude\claude_desktop_config.json` |
    | Linux | `~/.config/Claude/claude_desktop_config.json` |
    {: caption="Configuration file location" caption-side="bottom"}

To configure the agent:

1. Open the configuration file in a text editor.
2. Add the following configuration, replacing placeholder values with your actual credentials:

     ```bash
     {
       "mcpServers": {
         "IBM watsonx.data MCP Server": {
           "command": "/path/to/ibm-watsonxdata-mcp-server",
           "args": ["--transport", "stdio"],
           "env": {
             "WATSONX_DATA_BASE_URL": "https://<console-host>.lakehouse.cloud.ibm.com/lakehouse/api",
             "WATSONX_DATA_API_KEY": "<your_api_key_here>",
             "WATSONX_DATA_INSTANCE_ID": "crn:v1:<bluemix:public:lakehouse:us-south/a/...>"
           }
         }
       }
     }
     ```
     {: codeblock}

3. Save the file.
4. Restart the agent.

# Next steps
{: #remote-querying-data-ai-rmcp-nxt1}

- **Configure tools:** For detailed information on MCP tools and their usage, see [https://github.com/IBM/ibm-watsonxdata-mcp-server/blob/main/TOOLS.md](https://github.com/IBM/ibm-watsonxdata-mcp-server/blob/main/TOOLS.md).
