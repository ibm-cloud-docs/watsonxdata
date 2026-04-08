---

copyright:
  years: 2022, 2025
lastupdated: "2026-04-08"

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

# Getting start with the remote MCP server
{: #remote-querying-data-ai-end}

To connect your AI agent with {{site.data.keyword.lakehouse_short}} tools, you must obtain the endpoint for the remote MCP server.

## Prerequisites
{: #remote-querying-data-ai-en-pre}

Before connecting to the Remote MCP Server, ensure you have:

- **{{site.data.keyword.lakehouse_short}} instance** - A provisioned and running instance

   - [Provision a lite plan instance](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-tutorial_prov_lite_1) or [Provision an enterprice plan instance](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-getting-started_1)

   - [Set up {{site.data.keyword.lakehouse_short}} lite plan](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-tutorial_hp_intro)

- **IBM Cloud API key** - An API key with appropriate permissions to access your {{site.data.keyword.lakehouse_short}} instance. To create IBM Cloud API key, see [Creating an API key](https://cloud.ibm.com/docs/account?topic=account-userapikey&interface=ui#create_user_key).

- **Bearer token** - If remote MCP server using a Bearer token, you must generate a Bearer token. To generate Bearer token, refer [Generating an IBM Cloud IAM token by using an API key](https://cloud.ibm.com/docs/account?topic=account-iamtoken_from_apikey&interface=ui).

- **ApiKey authorization token** - The API key cannot be used directly; you must generate a Base64‑encoded authorization token.

   1. Build the credential string using the following format.

     ```bash
     ibmlhapikey_<your-email>:<your-apikey>
     ```
     {: codeblock}

     Example:

     ```bash
     ibmlhapikey_john.doe@ibm.com:abcd1234apikey
     ```

   2. Open a terminal on your system and run the following command.

     Mac or Linux:

     ```bash
     echo -n "ibmlhapikey_<your-email>:<your-apikey>" | base64
     ```
     {: codeblock}


     Example:

     ```bash
     echo -n "ibmlhapikey_john.doe@ibm.com:abcd1234apikey" | base64
     ```

     Windows PowerShell:

     ```bash
     [Convert]::ToBase64String([Text.Encoding]::ASCII.GetBytes("ibmlhapikey_<your-email>:<your-apikey>"))
     ```
     {: codeblock}

     Example:

     ```bash
     [Convert]::ToBase64String([Text.Encoding]::ASCII.GetBytes("ibmlhapikey_john.doe@ibm.com:abcd1234apikey"))
     ```

   3. Use the encoded value in the configuration file in the following format.

     ```bash
     authorization: Basic <base64-encoded-value>
     ```
     {: codeblock}

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

`https://<console-host>/api/v1/watsonxdata/mcp`

Replace the `<console-host>` placeholder with the appropriate value for your location from the following list:

- Sydney, Australia (Asia Pacific): `console-ibm-ausyd.lakehouse.saas.ibm.com`
- Toronto, Canada (North America): `console-ibm-cator.lakehouse.saas.ibm.com`
- Frankfurt, Germany (Europe): `eu-de.lakehouse.cloud.ibm.com`
- London, United Kingdom (Europe): `eu-gb.lakehouse.cloud.ibm.com`
- Tokyo, Japan (Asia Pacific): `jp-tok.lakehouse.cloud.ibm.com`
- Washington DC, USA (North America): `us-east.lakehouse.cloud.ibm.com`
- Dallas, USA (North America): `us-south.lakehouse.cloud.ibm.com`


### Connect your Agents with remote MCP Server
{: #remote-querying-data-ai-cng}

After connecting the remote MCP server, configure your agents to connect to the server. See the following topics for specific instructions:

- [Configuring Claude Desktop](/docs/watsonxdata?topic=watsonxdata-configuring-claude)
- [Configuring IBM Bob](/docs/watsonxdata?topic=watsonxdata-configuring-bob)
- [Configuring other MCP clients](/docs/watsonxdata?topic=watsonxdata-configuring-other-agents)

### Using the MCP tool
{: #remote-querying-data-ai-qdw}

For detailed information on MCP tools and their usage, refer [https://github.com/IBM/ibm-watsonxdata-mcp-server/blob/main/TOOLS.md](https://github.com/IBM/ibm-watsonxdata-mcp-server/blob/main/TOOLS.md).
