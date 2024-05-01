---

copyright:
  years: 2022, 2024
lastupdated: "2024-04-30"

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

# Registering an engine
{: #reg_engine}

{{site.data.keyword.lakehouse_full}} allows you to register engines that {{site.data.keyword.lakehouse_short}} does not directly manage, provision, or control.
{: shortdesc}

You can register the following engines:

   * IBM Db2 Warehouse
   * IBM Netezza
   * IBM Analytics Engine (Spark)


To register external engines, complete the following steps.

1. Log in to {{site.data.keyword.lakehouse_short}} console.

2. From the navigation menu, select **Infrastructure manager**.

3. To register an engine, click **Add component** and select **Add engine**.

4. In the **Add engine** window, select an engine from the **Type** drop-down list.

5. Based on the engine type you select, click one of the following links to configure the engine details.

    * [IBM Analytics Engine (Spark)](#sprk)
    * [IBM Db2 Warehouse](#DB2)
    * [IBM Netezza](#Netezza)




    * **IBM Analytics Engine (Spark)**{: #sprk}

      For **IBM Analytics Engine (Spark)**, configure the following details:

      | Field      | Description    |
      |--------------------------------|--------------------------------------------------------------------------------------------|
      | Display name   | Enter your compute engine name.  |
      | Instance API endpoint | Enter the IBM Analytics engine instance endpoint. For more information, see [Retrieving service endpoints](https://cloud.ibm.com/docs/AnalyticsEngine?topic=AnalyticsEngine-retrieve-endpoints-serverless)  |
      | API key   | Enter the API key. |
      {: caption="Table 1. Registering IBM Analytics Engine (Spark)" caption-side="bottom"}





    * **IBM Db2 Warehouse**{: #DB2}

      For **IBM Db2 Warehouse**, configure the following details:

      | Field      | Description    |
      |--------------------------------|--------------------------------------------------------------------------------------------|
      | Display name   | Enter your compute engine name.  |
      | Instance URL | Enter the console URL for **IBM Db2 Warehouse**.  |
      | Complete watsonx.data configuration in **IBM Db2 Warehouse**  | External engines require additional {{site.data.keyword.lakehouse_short}} configuration. For more information, see [How to configure watsonx.data in IBM Db2 Warehouse](https://www.ibm.com/docs/en/db2woc?topic=tables-accessing-watsonxdata). |
      | Confirmation check box | Select the confirmation check box to confirm complete configuration. |
      {: caption="Table 2. Registering IBM Db2 Warehouse" caption-side="bottom"}




    * **IBM Netezza**{: #Netezza}

      For **IBM Netezza**, configure the following details:

      | Field      | Description    |
      |--------------------------------|--------------------------------------------------------------------------------------------|
      | Display name   | Enter your compute engine name.  |
      | Instance URL | Enter the console URL for **IBM Netezza**.  |
      | Complete watsonx.data configuration in **IBM Netezza**  | External engines require additional {{site.data.keyword.lakehouse_short}} configuration. For more information, see [How to configure watsonx.data in IBM Netezza](https://cloud.ibm.com/docs/netezza?topic=netezza-integratenps_watsonx.data). |
      | Confirmation check box | Select the confirmation check box to confirm complete configuration. |
      {: caption="Table 3. Registering IBM Netezza" caption-side="bottom"}

6. Click **Register** to register the engine.
