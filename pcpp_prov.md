---

copyright:
  years: 2017, 2025
lastupdated: "2025-08-26"

keywords: watsonx.data, spark, emr
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Provisioning a Presto (C++) engine
{: #pcpp_prov}

An engine in {{site.data.keyword.lakehouse_short}} runs SQL queries on your data source and fetches the queried data. Presto (C++) is one of the engines supported in watsonx.data.

## Procedure
{: #pcpp_prov_pros}

1. Log in to the {{site.data.keyword.lakehouse_short}} console.
1. From the navigation menu, select **Infrastructure Manager**.
1. Click **Add component**, select **IBM Presto**, and click **Next**.
1. In the **Add component - IBM Presto** window, provide the following details to sign up new compute to work with your data:

    | Field | Description |
    | --- | --- |
    | Type | Select the **Presto (C++)** engine from the list. |
    | Display name   | Enter your compute engine name.  |
    | Configuration mode | **Standard**: Select **Standard** for predefined engine sizes: |
    |   |**Starter**: Includes 1 coordinator node and 1 worker node, both starter.   |
    |   | **Small**: Includes 1 coordinator node and 3 worker nodes, all cache-optimized.  |
    |   | **Medium**: Includes 1 coordinator node and 6 worker nodes, all cache-optimized.  |
    |   |**Large**: Includes 1 coordinator node and 12 worker nodes, all cache-optimized.  |
    |   | **Custom**: Select **Custom** for customized engine configuration:    |
    |    |  **Coordinator nodes (max. 1)**: Select the run rate for coordinator node (you can have a maximum of 1 node).  |
    |    |  **Worker nodes (max. 18)**: Select the number of worker nodes and run rate (you can have a maximum of 18 nodes).  |
    | Associated catalogs (optional) | Associate the available catalogs with the engine if necessary.  |
    {: caption="Add engine details" caption-side="bottom"}

1. Click **Create**.

## Related API
{: #pcpp_api}

For information on related API, see
* [Get list of Presto (C++) engines](https://cloud.ibm.com/apidocs/watsonxdata#list-prestissimo-engines)
* [Create Presto (C++) engine](https://cloud.ibm.com/apidocs/watsonxdata#create-prestissimo-engine)
* [Get Presto (C++) engine](https://cloud.ibm.com/apidocs/watsonxdata#get-prestissimo-engine)
* [Pause a Presto (C++) engine](https://cloud.ibm.com/apidocs/watsonxdata#pause-prestissimo-engine)
* [Restart a Presto (C++) engine](https://cloud.ibm.com/apidocs/watsonxdata#restart-prestissimo-engine)
* [Resume a Presto (C++) engine](https://cloud.ibm.com/apidocs/watsonxdata#resume-prestissimo-engine)
* [Scale a Presto (C++) engine](https://cloud.ibm.com/apidocs/watsonxdata#scale-prestissimo-engine)
