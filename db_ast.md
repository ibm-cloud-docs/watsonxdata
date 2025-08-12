---

copyright:
  years: 2022, 2025
lastupdated: "2025-08-12"

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

# {{site.data.keyword.lakehouse_short}} assistant - gen AI powered chat interface
{: #db_ast}


{{site.data.keyword.lakehouse_full}} assistant, a gen AI powered chat interface built with IBM watsonx™. It seamlessly provides information about {{site.data.keyword.lakehouse_short}} using the product knowledge.

You can chat with the {{site.data.keyword.lakehouse_short}} assistant to ask questions about {{site.data.keyword.lakehouse_full}}. The assistant answers your queries about {{site.data.keyword.lakehouse_short}} based on its knowledge on IBM product documentation. It helps to explore and learn about the product in an easier and faster way.


## Enabling {{site.data.keyword.lakehouse_short}} assistant
{: #db_bfb_enab}

To start using {{site.data.keyword.lakehouse_short}} assistant, the administrator must enable the feature.

1. Log in to the {{site.data.keyword.lakehouse_short}} instance.
1. Go to **Configurations**.
1. Click **watsonx.data assistant**. The **watsonx.data assistant** page opens.
1. Toggle **Enable watsonx.data assistant** option to enable **watsonx.data assistant**.

## Starting the {{site.data.keyword.lakehouse_short}} assistant
{: #db_bfb_strt}

To get started with the {{site.data.keyword.lakehouse_short}} assistant:


1. Log in to the {{site.data.keyword.lakehouse_short}} instance.
1. Click the **AI** icon on the top right of the {{site.data.keyword.lakehouse_short}} home page to launch **watsonx.data assistant**.
1. Type your questions and requests in the chat.

1. Review the generated response.

1. Provide feedback for the response and help improve the assistant. You have the following feedback options:
   * Good response : You can select this option if you are satisfied with the response.
   * Bad response : You can select this option if the response has to be improved. The chat prompts you for additional feedback.


## What can the {{site.data.keyword.lakehouse_short}} assistant do?
{: #db_bfb_strt2}


   | Category | Action | Description | Example prompt phrases |
   |-------------|-------------|-----|----|
   | Product Documentation | Answer your queries related to {{site.data.keyword.lakehouse_short}}. | Ask the assistant anything about {{site.data.keyword.lakehouse_short}} and it will generate an answer based on its knowledge of the product. The assistant uses Generative AI to generate the responses.| - How to provision milvus in {{site.data.keyword.lakehouse_short}}? \n - What data sources are supported in {{site.data.keyword.lakehouse_short}} for Arrow Flight Service \n - How do you access Spark logs for an ingested job? \n - How to edit engine details?|
   {: caption="What can the assistant do?" caption-side="bottom"}
