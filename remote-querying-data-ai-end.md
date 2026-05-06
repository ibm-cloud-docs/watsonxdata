---

copyright:
  years: 2022, 2025
lastupdated: "2026-05-06"

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

To set up the remote MCP server with your local host, you add the MCP server information to the host configuration file. You can obtain the configuration information from the watsonx.data web console (recommended) or manually gather it from IBM Cloud.

## Getting the required credentials and instance information
{: #remote-querying-data-ai-en-pre}

You can obtain the required MCP server credentials and instance information by using one of the following options:

### Getting configuration from the web console
{: #getting-mcp-config-console}

You can obtain the MCP URL endpoint, instance CRN, and pre-configured code snippets directly from the watsonx.data web console.

To get the configuration from the web console:

1. Log in to your watsonx.data web console.
2. From the navigation menu, select **Configurations** and click **MCP server**.
4. From the **MCP configuration** section, select the appropriate option based on your host type:

      - **Bob**: Configuration for IBM Bob host
      - **Claude**: Configuration for Claude Desktop
      - **Other**: Generic configuration for other MCP-compatible clients

5. Copy the complete configuration snippet displayed. The snippet includes all required credentials except the Base64-encoded key.

6. Create the Base64-encoded key:
   1. If you do not have an existing API key, click **API key** to create your API key. For more information, see [Creating an API key](https://cloud.ibm.com/docs/account?topic=account-userapikey&interface=ui#create_user_key){: external}.
   2. Transform your API key into a Base64-encoded value as described in [Creating a base64 credential string](#getting-mcp-config-base64).
   3. Replace the `<base64-encoded-value>` placeholder in the configuration snippet with your encoded value.

### Manually gathering configuration information
{: #getting-mcp-config-manual}

Alternatively, you can manually gather the required configuration information from IBM Cloud and build the configuration yourself.

You need to provide values for the following variables in the host configuration file:

- The `<console-host>` portion of your {{site.data.keyword.lakehouse_short}} instance URL for the MCP server endpoint, which has the following format: </br>`https://<console-host>/api/v1/watsonxdata/mcp`
- Your credentials:

   - Your IBM Cloud API key in a base64 credentials string OR your IBM Cloud bearer token

- The Cloud Resource Name (CRN) of your {{site.data.keyword.lakehouse_short}} instance

To get your credentials and instance information:

1. Log into IBM Cloud.
2. To find the `<console-host>` and CRN values, go to **Resources list** from the navigation menu and select your {{site.data.keyword.lakehouse_short}} instance from **Database** dropdown.
3. Get the value of `<console-host>` by copying the first part of the web console URL. For example: `console-ibm-cator.lakehouse.saas.ibm.com`
4. Get your {{site.data.keyword.lakehouse_short}} instance CRN by copying the CRN value. The CRN has the following format: `crn:v1:bluemix:public:lakehouse:us-south/a/...`
5. Create the Base64-encoded key:
   1. If you do not have an existing API key, create your API key. For more information, see [Creating an API key](https://cloud.ibm.com/docs/account?topic=account-userapikey&interface=ui#create_user_key){: external}.
   2. Transform your API key into a Base64-encoded value as described in [Creating a base64 credential string](#getting-mcp-config-base64).

6. If you want to use your IBM Cloud bearer token as your authorization credentials, copy or generate your bearer token. See [Generating an IBM Cloud IAM token by using an API key](https://cloud.ibm.com/docs/account?topic=account-iamtoken_from_apikey&interface=ui){: external}.

### Creating a base64 credential string
{: #getting-mcp-config-base64}

Open a terminal and run the following command, replacing the placeholders with your values:

- Mac or Linux

   ```bash
    echo -n "ibmlhapikey_<your-email>:<your-apikey>" | base64
   ```
   {: codeblock}

- Windows PowerShell

   ```bash
    [Convert]::ToBase64String([Text.Encoding]::ASCII.GetBytes("ibmlhapikey_<your-email>:<your-apikey>"))
   ```
   {: codeblock}

## Configuring the host
{: #remote-querying-data-ai-rmcp}

After obtaining the configuration information, you need to add it to your host's configuration file.

- The IBM Bob configuration file is:

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

- For other hosts, you must determine the appropriate file for the local MCP server configuration.

To configure the host:

1. Open the configuration file in a text editor.
2. Add the configuration:

   - **If you used the web console:** Paste the complete configuration snippet you copied from the web console.

   - **If you manually gathered the information:** Add the appropriate configuration based on your host type and credentials, and replace the placeholder values with your actual credentials gathered from IBM Cloud:

     **For Bob and other MCP-compatible hosts (using API credentials):**

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

     **For Claude (using API credentials):**

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

     **For Claude and Bob (using bearer token):**

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

3. Save the file.
4. Restart the host.

## Next steps
{: #remote-querying-data-ai-rmcp-nxt1}

- **Configure tools:** For detailed information on MCP tools and their usage, see [https://github.com/IBM/ibm-watsonxdata-mcp-server/blob/main/TOOLS.md](https://github.com/IBM/ibm-watsonxdata-mcp-server/blob/main/TOOLS.md).
