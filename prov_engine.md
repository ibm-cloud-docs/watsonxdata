---

copyright:
  years: 2022, 2025
lastupdated: "2025-08-26"

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

# Provisioning a Presto (Java) engine
{: #prov_engine}

An engine in {{site.data.keyword.lakehouse_short}} runs SQL queries on your data source and fetches the queried data. Presto (Java) is one of the engines supported in watsonx.data.

To provision a Presto (Java) engine, complete the following steps.
{: shortdesc}

1. Log in to {{site.data.keyword.lakehouse_short}} console.

2. From the navigation menu, select **Infrastructure manager**.

3. Click **Add component**, select **IBM Presto**, and click **Next**.

4. In the **Add component - IBM Presto** window, provide the following details to sign up new compute to work with your data:

   | Field      | Description    |
   |--------------------------------|--------------------------------------------------------------------------------------------|
   | Type | Select the **Presto (Java) (version)** engine from the list. |
   | Display name   | Enter your compute engine name.  |
   | Configuration mode | **Standard:** Select **Standard** for predefined engine sizes:  |
   |    |  **Lite**: Includes 1 coordinator node. **Note**: The Presto (Java) Lite mode is available only in {{site.data.keyword.lakehouse_short}} Lite plan. |
   |    |  **Starter**: Includes 1 coordinator node and 1 worker node, both starter. **Note**: The Starter mode is not available for a Presto (Java) engine in {{site.data.keyword.lakehouse_short}} Lite plan.   |
   |    |  **Small**: Includes 1 coordinator node and 3 worker nodes, all cache-optimized.  |
   |    |  **Medium**: Includes 1 coordinator node and 6 worker nodes, all cache-optimized.  |
   |    |  **Large**: Includes 1 coordinator node and 12 worker nodes, all cache-optimized.  |
   |    |  **Custom**: Select **Custom** for customized engine configuration:  |
   |    |  **Coordinator nodes (max. 1)**: Select the run rate for coordinator node (you can have a maximum of 1 node).  |
   |    |  **Worker nodes (max. 18)**: Select the number of worker nodes and run rate (you can have a maximum of 18 nodes).  |
   | Associated catalogs (optional) | Associate the available catalogs with the engine if necessary. HANA and MySQL catalogs do not display due to the Bring Your Own JAR (BYOJ) process. |
   {: caption="Provision engine" caption-side="bottom"}

5. Click **Create**.

[def]: https://prestodb.io/docs/0.279/
[def1]: https://prestodb.io/docs/0.282/
[def2]: https://prestodb.io/docs/0.285.1/
[def3]: https://prestodb.io/docs/0.286/

## Related API
{: #presto_api}

For information on related API, see
* [Get list of Presto (Java) engines](https://cloud.ibm.com/apidocs/watsonxdata#list-presto-engines)
* [Create Presto (Java) engine](https://cloud.ibm.com/apidocs/watsonxdata#create-presto-engine)
* [Get Presto (Java) engine](https://cloud.ibm.com/apidocs/watsonxdata#get-presto-engine)
* [Pause a Presto (Java) engine](https://cloud.ibm.com/apidocs/watsonxdata#pause-presto-engine)
* [Restart a Presto (Java) engine](https://cloud.ibm.com/apidocs/watsonxdata#restart-presto-engine)
* [Resume a Presto (Java) engine](https://cloud.ibm.com/apidocs/watsonxdata#resume-presto-engine)
* [Scale a Presto (Java) engine](https://cloud.ibm.com/apidocs/watsonxdata#scale-presto-engine)
