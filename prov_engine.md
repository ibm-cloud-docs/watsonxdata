---

copyright:
  years: 2022, 2023
lastupdated: "2023-09-27"

keywords: lakehouse, engine, watsonx.data
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

# Creating an engine
{: #prov_engine}

To create an engine, complete the following steps.
{: shortdesc}

1. Log in to {{site.data.keyword.lakehouse_short}} console.

2. From the navigation menu, select **Infrastructure manager**.

3. To provision an engine, click **Add component** and select **Create engine**.

4. In the **Create engine** window, provide the following details to a sign up new compute to work with your data.

   | Field      | Description    |
   |--------------------------------|--------------------------------------------------------------------------------------------|
   | Type    | Select the engine type from the list.   |
   | Display name   | Enter your compute engine name.  |
   | Configuration mode | Select Quick for predefined engine sizes or Custom for customized engine configuration.  |
   | Size   | Select the engine size. For all sizes, coordinator and worker nodes are storage-optimized. |
   | Catalogs associated (optional) | Associate the available catalogs with the engine if necessary.  |
   {: caption="Table 1. Provision engine" caption-side="bottom"}

5. Click **Create**.
