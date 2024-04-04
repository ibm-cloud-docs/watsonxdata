---

copyright:
  years: 2022, 2024
lastupdated: "2024-04-03"

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

# Provisioning a Presto engine
{: #prov_engine}

To provision a Presto engine, complete the following steps. For more information about Presto engine, see [Presto overview](watsonxdata?topic=watsonxdata-presto_overview).
{: shortdesc}

1. Log in to {{site.data.keyword.lakehouse_short}} console.

2. From the navigation menu, select **Infrastructure manager**.

3. To provision an engine, click **Add component** and select **Add engine**.

4. In the **Add engine** window, select **Presto(version)** from the **Type** drop-down list.

5. Configure the following engine details.

   | Field      | Description    |
   |--------------------------------|--------------------------------------------------------------------------------------------|
   | Display name   | Enter your compute engine name.  |
   | Configuration mode | Select Standard for predefined engine sizes or Custom for customized engine configuration.  |
   | Size   | Select the engine size. For all sizes, coordinator and worker nodes are storage-optimized. The field appears when you select the **Configuration mode** as **Standard**. |
   | Coordinator nodes (max.1) | Select the size for the coordinator node. The field appears when you select the **Configuration mode** as **Custom**. |
   | Worker nodes (max.18) | Select the size required for worker node. The field appears when you select the **Configuration mode** as **Custom**.|
   | Associated Catalogs (optional) | Associate the available catalogs with the engine if necessary.  |
   {: caption="Table 1. Provision engine" caption-side="bottom"}


5. Click **Provision(0+RUs/hour)** to provision the Presto engine.
