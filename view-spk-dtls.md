---

copyright:
  years: 2022, 2024
lastupdated: "2024-04-30"

keywords: lakehouse, engine, tags, description, watsonx.data

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

# Managing the Spark engine details
{: #view-end}

{{site.data.keyword.lakehouse_full}} allows you to view and edit the details of a Spark engine. You can also monitor the status of the applications that are submitted in the instance.
{: shortdesc}

## Viewing the Spark engine details
{: #view-dtls}

You can view the Spark details in list and topology views.

1. Click the name of Spark engine (either from list or topology view). Engine information window opens.
2. In the **Details** tab, you can view the following details:


   | Field      | Description    |
   |--------------------------------|--------------------------------------------------------------------------------------------|
   | Display name   | The Spark engine name.  |
   | Engine ID | The unique identifier of the Spark instance.  |
   | Description   | The description of the engine. |
   | Tags | The tag that is specified at the time of registering an engine. |
   | Type | The engine type. Here, IBM Analytics Engine (Spark). |
   | Instance URL | The IBM Analytics Engine (Spark) URL.  |
   | watsonx.data application endpoint| The application submission endpoint. To submit an application by using API, see [API Docs](https://cloud.ibm.com/apidocs/watsonxdata-software).|
   | Instance API endpoint | The IBM Analytics Engine (Spark) API endpoint.|
   | History server endpoint| The IBM Analytics Engine (Spark) history server endpoint.|
   | History server | The history server URL, where you can view the history details of the applications that are run.|
   {: caption="Table 1. Details tab" caption-side="bottom"}


## Editing the Spark engine details
{: #edit-dtls}


You can edit the Spark details in list and topology views.

1. Click the name of Spark engine (either from list or topology view). Engine information window opens.
2. In the **Details** tab, click **Edit**.
3. In the **Display name** field, enter the display name for the Spark engine.
3. In the **Description** field, enter the description of the engine or edit the existing description.
4. In the **Tags** field, select the tags from the list or start typing to define a new tag.
5. Click **Save**.

## Viewing the Spark applications submitted in {{site.data.keyword.lakehouse_short}}
{: #sub-appl-dtls}


You can view the status of the submitted Spark applications in list and topology views.

1. Click the name of the Spark engine (either from list or topology view). Engine information window opens.
2. In **Applications** tab, you can view the list of all applications that are submitted to {{site.data.keyword.lakehouse_short}}. The tab also displays the details such as the status of each application, the Spark version used for running the application, creation date, and run date.
