---

copyright:
  years: 2022, 2025
lastupdated: "2026-03-31"

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

# Configuring IBM Bob to connect to the MCP server
{: #configuring-bob}

After you install the MCP server on your local machine, you must configure IBM Bob to connect to the MCP server.

## Configuration file location
{: #configuring-bob-cfl}

The IBM Bob configuration file is located at:

   ```bash

   ~/Library/Application Support/Bob-IDE/User/globalStorage/ibm.bob-code/settings/mcp_settings.json
   ```

## Configuration procedure
{: #configuring-bob-cp}


1. Open the IBM Bob configuration file in a text editor.

2. Add the following configuration, replacing placeholder values with your actual credentials:

   - **For remote MCP server use the following configuration**

     ```bash
     {
     "mcpServers": {
     "watsonx-data-gateway": {
     "command": "npx",
     "args": [
     "-y",
     "mcp-remote",
     "https: <PLACEHOLDER>",
     "--header",
     "apikey: <YOUR_IBM_CLOUD_API_KEY>",
     "--header",
     "authinstanceid: <YOUR_WATSONXDATA_INSTANCE_CRN>"
     ]
     }
     }
     }
     ```
     {: codeblock}

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

4. Restart IBM Bob.
