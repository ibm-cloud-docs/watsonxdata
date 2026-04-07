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

# Configuring other MCP clients to connect to the remote MCP server
{: #configuring-other-agents}

You can integrate the {{site.data.keyword.lakehouse_short}} remote MCP Server with any client that supports the Model Context Protocol (MCP). This integration enables your agents and applications to securely interact with {{site.data.keyword.lakehouse_short}} lakehouse environments through a standardized interface.

Use the following generic configuration to connect your MCP-compatible client to remote server.



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

 <br>- Refer your remote MCP client documentation to locate the configuration file path. <br> - The JSON structure is consistent across most clients. However, some clients might use different root keys (for example, `"mcp"` instead of `"mcpServers"`).<br> - Ensure that all required authentication headers are correctly configured for your watsonx.data instance.<br> - Replace placeholder values with your actual credentials and instance information.<br> - The `<console-host>` value is location specific. For the appropriate value to use, see [Remote MCP server endpoint](/docs/watsonxdata?topic=watsonxdata-remote-querying-data-ai-end#remote-querying-data-ai-rmcp)
 {: note}
