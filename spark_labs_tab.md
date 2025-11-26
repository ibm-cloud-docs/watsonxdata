---

copyright:
  years: 2022, 2025
lastupdated: "2025-11-26"

keywords: lakehouse, watsonx data, roles, access
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


# Managing Spark labs from Console
{: #lab_console}

The **Spark labs** tab in the watsonx.data console lets you monitor and manage labs directly from the console, while lab creation remains available through the VS Code extension. It displays key details for each lab and provides controls to review, filter, and stop labs when needed.
{: shortdesc}


1. Log in to the {{site.data.keyword.lakehouse_short}} cluster and go to the **Infrastructure manager** page.
1. Click on the name of the Spark engine (either from list or topology view). The **Engine information** window opens.
1. Click the **Spark labs** tab. It displays a table with the list of Spark labs. You can view the following details:


   | Field           | Description        |
   |------------------|--------------------|
   | Name     | The name of the Spark Lab. |
   |ID          | Unique identifier for the lab.|
   |Status  | Current state of the lab (e.g., ACTIVE, FAILED, STOPPED).|
   | Created On      | Timestamp when the lab was created. |
   | Started On          | Timestamp when the lab started running. |
   | Stopped On            | Timestamp when the lab was stopped (if applicable). |
   {: caption="Spark labs" caption-side="bottom"}


The table defaults to showing **ACTIVE Spark labs** only. Other statuses (FAILED, STOPPED) are hidden by default but can be revealed by adjusting filters.
{: note}

## Stopping a Spark lab
{: #stoplab}

You can stop an active Spark lab directly from the console. A confirmation popup warns that stopping the lab will **delete extensions and user data within the lab**.


Click **View VS Code Configuration** button to access the configuration details for integration with VS Code.
