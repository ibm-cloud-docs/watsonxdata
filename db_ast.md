---

copyright:
  years: 2022, 2025
lastupdated: "2025-06-10"

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

# watsonx.data Assistant - genAI powered chat interface
{: #db_ast}


{{site.data.keyword.lakehouse_full}} Assistant, a gen AI-powered chat interface built with IBM watsonx™. It allows you to seamlessly retrieve information about IBM watsonx.data product information.

You can chat with the {{site.data.keyword.lakehouse_short}} Assistant to ask questions about {{site.data.keyword.lakehouse_full}}. Assistant answers your queries about {{site.data.keyword.lakehouse_short}} based on its knowledge on IBM product documentation. It helps to explore and learn about the product in an easier and faster way.



## Before you begin
{: #db_bfb}

### Enabling {{site.data.keyword.lakehouse_short}} Assistant
{: #db_bfb_enab}

To start using {{site.data.keyword.lakehouse_short}} Assistant, the administrator must enable the feature.

1. Log in to the watsonx.data instance.
1. Go to **Configurations**.
1. Click **Watsonx Data Assistant**.
1. Clcik **Edit**. The **Edit Watsonx.data Assistant** page opens.
1. Select **Enable Watsonx Data Assistant** checkbox.
1. Click **Save**.


## Starting the database assistant
{: #db_bfb_strt}

To get started with the database assistant:


1. Log in to the watsonx.data instance.

1. Click the **AI** **(AI Assistant)** icon on the top right of the {{site.data.keyword.lakehouse_short}} home page to launch **Watsonx Data Assistant**.

1. Type your questions and requests in the chat.

1. Review the generated response.

1. Provide feedback for the response and help improve the assistant. You have the following feedback options:
   * Good response : You can select this option if you are happy with the response.
   * Bad response : You can select this option if you are unhappy with the response. The chat prompts you for additional feedback.



## What can the assistant do?
{: #db_bfb_strt2}


   | Category | Action | Description | Example prompt phrases |
   |-------------|-------------|-----|----|
   | Product Documentation | Answer your queries related to watsonx data. | Ask the assistant anything about watsonx data and it will generate an answer based on its knowledge of the product. The assistant uses Generative AI to generate the responses.| - How to provision milvus in watsonx data? \n - What data sources are supported in watsonx.data for Arrow Flight Service \n - How do you access Spark logs for an ingested job? \n - How to edit engine details?|
   {: caption="What can the assistant do?" caption-side="bottom"}
