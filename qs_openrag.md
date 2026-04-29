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
- Your OpenRAG sign-in credentials:
  - **Username**: Follows the pattern `ibmlhapikey_<ibm-email>`. For example, `ibmlhapikey_john.doe@ibm.com`.
  - **Password**: Your IBM Cloud API key. To create or retrieve an API key, go to [IBM Cloud API keys](https://cloud.ibm.com/iam/apikeys){: external}.
- Credentials for at least one supported language model provider:
  - Anthropic API key
  - OpenAI API key
  - IBM watsonx.ai API endpoint, project ID, and API key
- Credentials for at least one supported embedding model provider:
  - OpenAI API key
  - IBM watsonx.ai API endpoint, project ID, and API key

## Provision OpenRAG and OpenSearch
{: #setup-openrag-from-home-task}

Complete the following steps to provision and configure OpenRAG:

1. Open the {{site.data.keyword.lakehouse_short}} web console.
1. On the welcome page, select the tile that matches your goal.
1. To use OpenRAG, select **Develop RAG pipelines that connect LLMs to your data**, and then click **Next**.

   The OpenRAG tile is displayed only if IBM enabled the private preview on your cluster.
   {: note}

1. On the **Configure Details** page, define the details to configure OpenRAG.
1. Keep the **Starter** cluster selection, which is selected by default.
1. Review the configuration. OpenSearch is required for OpenRAG and is added automatically when you provision OpenRAG.
1. Click **Finish and go** to start provisioning.

If provisioning is still in progress, the console redirects you to the **Infrastructure Manager** page so that you can monitor status. If provisioning is complete, the home page is displayed.

After provisioning is complete, sign in to OpenRAG.

1. On the home page, select the **OpenRAG** tile.
1. Enter your OpenRAG **Username** and **Password**, and then click **Continue**.
   - Your username follows the pattern `ibmlhapikey_<ibm-email>`. For example, `ibmlhapikey_john.doe@ibm.com`.
   - Your password is your IBM Cloud API key. To create or retrieve an API key, go to https://cloud.ibm.com/iam/apikeys.

1. On the OpenRAG onboarding page, set up the language model and embedding model providers.
1. Select a language model provider from the available options:
   - Anthropic
   - OpenAPI
   - IBM watsonx.ai
1. Enter the credentials for the selected provider, choose a language model from the dropdown, and then click **Complete**.
1. Wait for OpenRAG to verify the provider credentials and open the embedding provider step. The following embedding providers are available:
   - OpenAI
   - IBM watsonx.ai
1. Enter the credentials for the embedding provider, select an embedding model from the list, and then click **Complete**.
1. Wait while OpenRAG ingests the default documents. You can change the language model and embedding model settings later from the OpenRAG **Settings** page.
1. After ingestion is complete, click **What is OpenRAG?** to run your first query.
1. Confirm that the query runs successfully.
1. Choose what you want to do next:
   - Click **Add a document** to ingest another document source.
   - Click **Skip overview** to open the OpenRAG home page.

You have now completed the initial OpenRAG setup.
