---

copyright:
  years: 2022, 2025
lastupdated: "2026-04-07"

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

# Configuring Claude Desktop to connect to the MCP server
{: #configuring-claude}

After you install the MCP server on your local machine, you must configure Claude Desktop to connect to the MCP server.

## Locating the configuration file
{: #configuring-claude-lcf}

The Claude Desktop configuration file location varies by operating system:

| Operating System | Configuration File Path |
|-----------------|-------------------------|
| macOS | `~/Library/Application Support/Claude/claude_desktop_config.json` |
| Windows | `%APPDATA%\Claude\claude_desktop_config.json` |
| Linux | `~/.config/Claude/claude_desktop_config.json` |
{: caption="Configuration file location" caption-side="bottom"}

## Configuration procedure
{: #configuring-claude-cp}


1. Open the Claude Desktop configuration file in a text editor.

2. Add the following configuration, replacing placeholder values with your actual credentials:

   - **For remote MCP server use the following configuration**

     ```bash
     {
       "mcpServers": {
         "watsonx.data-mcp-server": {
           "type": "streamable-http",
           "url": "https://<console-host>/api/v1/watsonxdata/mcp",
           "headers": {
             "authorization": "Basic <base64(ibmlhapikey_user@ibm.com:apikey)",
             "authinstanceid": "<YOUR_WATSONXDATA_INSTANCE_CRN>"
           }
         }
       }
     }
     ```
     {: codeblock}

     The `<console-host>` value is location specific. For the appropriate value to use, see [Remote MCP server endpoint](/docs/watsonxdata?topic=watsonxdata-remote-querying-data-ai-end#remote-querying-data-ai-rmcp).
     {: note}

   - **For local MCP server use the following configuration**

     ```bash
     {
       "mcpServers": {
         "IBM watsonx.data MCP Server": {
           "command": "/path/to/ibm-watsonxdata-mcp-server",
           "args": ["--transport", "stdio"],
           "env": {
             "WATSONX_DATA_BASE_URL": ""https://<your-instance>.lakehouse.cloud.ibm.com/lakehouse/api",
             "WATSONX_DATA_API_KEY": "<your_api_key_here>",
             "WATSONX_DATA_INSTANCE_ID": "crn:v1:<bluemix:public:lakehouse:us-south/a/...>"
           }
         }
       }
     }
     ```
     {: codeblock}

3. Save the configuration file.

4. Restart Claude Desktop.

To configure Claude Desktop for development setup, refer [IBM {{site.data.keyword.lakehouse_short}} MCP Server](https://github.com/IBM/ibm-watsonxdata-mcp-server?tab=readme-ov-file).
