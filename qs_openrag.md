---

copyright:
  years: 2026
lastupdated: "2026-04-29"

keywords: openrag, watsonx.data, opensearch, watsonx.ai, home page, setup, quick start

subcollection: watsonxdata

content-type: tutorial
services: watsonxdata
completion-time: 10m

---

{{site.data.keyword.attribute-definition-list}}

# Quick start: Provision OpenRAG and OpenSearch (Private preview)
{: #qs_openrag}
{: toc-content-type="tutorial"}
{: toc-services="watsonxdata"}
{: toc-completion-time="10m"}

This tutorial guides you through the initial configuration of OpenRAG in {{site.data.keyword.lakehouse_full}} to help you quickly start building AI-powered search applications with retrieval-augmented generation.
{: shortdesc}

OpenRAG combines OpenSearch with retrieval-augmented generation (RAG) technology to transform unstructured data into actionable context for AI applications. It enables semantic search, vector embeddings, and seamless integration with large language models.

## Before you begin
{: #setup-openrag-from-home-prereqs}

Before you start, make sure that you have:

- Access to the {{site.data.keyword.lakehouse_short}} web console
- Permission to provision services in your {{site.data.keyword.lakehouse_short}} environment
- Your OpenRAG user name and password
- Your watsonx.ai API endpoint and project ID

## Setting up OpenRAG
{: #setup-openrag-from-home-task}

Complete the following steps to provision and configure OpenRAG:

1. Open the {{site.data.keyword.lakehouse_short}} web console.
1. On the welcome page, select the tile that matches your goal.
1. To use the OpenRAG service, select **Develop RAG pipelines that connect LLMs to your data**, and then click **Next**.
1. On the **Configure Details** page, define the details to configure OpenRAG.
1. Keep the **Starter** cluster selection, which is selected by default.
1. Review the configuration. OpenSearch is added automatically when you add OpenRAG.
1. Click **Finish and go**.
1. Wait for the {{site.data.keyword.lakehouse_short}} console home page to open.
1. On the home page, select the **OpenRAG for .data** tile.
1. Enter your OpenRAG **Username** and **Password**, and then click **Continue**.
1. On the setup page, set up your LLM provider.
1. Review the available provider options:
    - Anthropic
    - OpenAPI
    - IBM watsonx.ai
1. Select **IBM watsonx.ai**.
1. Complete the following fields:
    - **watsonx.ai API Endpoint**
    - **watsonx ProjectID**
1. Choose whether to use the environment API key:
    - To use the environment key, turn on **Use environment watsonx API key**.
    - To provide a key manually, leave the toggle off and enter your **watsonx API key**.
1. Click **Complete**.

After setup finishes, both the OpenSearch and OpenRAG services are provisioned and displayed on the **Infrastructure Manager** page. You can select a service to view its details page.

## Next steps
{: #setup-openrag-from-home-next}

After you complete the setup, you can:

- Review service status and details from the **Infrastructure Manager** page
- Continue with your OpenRAG workflow configuration.
