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

# Setting up the remote MCP server
{: #remote-querying-data-ai-end}

To set up the remote MCP server with your local agent, you add the MCP server information to the agent configuration file.

## Getting the required credentials and instance information
{: #remote-querying-data-ai-en-pre}

You need to provide values for the following variables in the agent configuration file:

- The `<console-host>` portion of your {{site.data.keyword.lakehouse_short}} instance URL for the MCP server endpoint, which has the following format: </br>`https://<console-host>/api/v1/watsonxdata/mcp`
- Your credentials:

   - Your IBM Cloud API key in a base64 credentials string
   - Your IBM Cloud bearer token

- The Cloud Resource Name (CRN) of your {{site.data.keyword.lakehouse_short}} instance

To get your credentials and instance information:

1. Log into IBM Cloud.
2. To find the `<console-host>` and CRN values, go to **Resources** and select your {{site.data.keyword.lakehouse_short}} instance.
3. Get the value of `<console-host>` by copying the first part of the web console URL. For example: `console-ibm-cator.lakehouse.saas.ibm.com`
4. Get your {{site.data.keyword.lakehouse_short}} instance CRN by copying the CRN value. The CRN has the following format: `crn:v1:bluemix:public:lakehouse:us-south/a/...`
5. If you want to use your IBM Cloud API key as your authorization credentials, follow these steps to create a base64 credential string:

    1. If you do not have an existing key, create your API key.See [Creating an API key](https://cloud.ibm.com/docs/account?topic=account-userapikey&interface=ui#create_user_key){: external}.
    2. Open a terminal and run the following command, replacing the placeholders with your values:

       - Mac or Linux:

         ```bash
          echo -n "ibmlhapikey_<your-email>:<your-apikey>" | base64
         ```
         {: codeblock}

       - Windows PowerShell:

         ```bash
          [Convert]::ToBase64String([Text.Encoding]::ASCII.GetBytes("ibmlhapikey_<your-email>:<your-apikey>"))
         ```
         {: codeblock}

6. If you want to use your IBM Cloud bearer token as your authorization credentials, copy or generate your bearer token. See [Generating an IBM Cloud IAM token by using an API key](https://cloud.ibm.com/docs/account?topic=account-iamtoken_from_apikey&interface=ui){: external}.

## Configuring the agent
{: #remote-querying-data-ai-rmcp}

You configure the agent to connect to the MCP server by editing the agent configuration file:

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

- For other agents, you must determine the appropriate file for the local MCP server configuration.

To configure the agent:

1. Open the configuration file in a text editor.
2. Add the following configuration, replacing placeholder values with your actual credentials:

   - **For API credentials:**

     ```bash
     {
       "mcpServers": {
         "watsonx.data-mcp-server": {
           "command": "npx",
           "args": [
             "mcp-remote",
             "https://<console-host>/api/v1/watsonxdata/mcp",
             "--header",
             "authorization: Basic <base64-encoded-value>",
             "--header",
             "authinstanceid: <YOUR_WATSONXDATA_INSTANCE_CRN>"
           ]
         }
       }
     }
     ```
     {: codeblock}

   - **For bearer token:**

     ```bash
         {
       "mcpServers": {
         "watsonx.data-mcp-server": {
           "command": "npx",
           "args": [
             "mcp-remote",
             "https://<console-host>/api/v1/watsonxdata/mcp",
             "--header",
             "authorization: Bearer <YOUR_TOKEN>",
             "--header",
             "authinstanceid: <YOUR_WATSONXDATA_INSTANCE_CRN>"
           ]
         }
       }
     }
     ```
     {: codeblock}

     - **For streamable-http type:**

     ```bash
     {
       "mcpServers": {
         "watsonx.data-mcp-server": {
           "type": "streamable-http",
           "url": "https://<console-host>/api/v1/watsonxdata/mcp",
           "headers": {
             "authorization": "Basic <base64-encoded-value>",
             "authinstanceid": "<YOUR_WATSONXDATA_INSTANCE_CRN>"
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
