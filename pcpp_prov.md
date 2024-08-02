---

copyright:
  years: 2017, 2024
lastupdated: "2024-08-02"

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
    | Type | Select the **Presto (C++) (version)** engine from the list. |
    | Display name   | Enter your compute engine name.  |
    | Configuration mode | **Standard:**<br>Select **Standard** for predefined engine sizes:<br> - **Starter:** Includes 1 coordinator node and 1 worker node, both starter.<br> - **Small:** Includes 1 coordinator node and 3 worker nodes, all cache-optimized.<br> - **Medium:** Includes 1 coordinator node and 6 worker nodes, all cache-optimized.<br> - **Large:** Includes 1 coordinator node and 12 worker nodes, all cache-optimized.<br>**Custom:**<br>Select **Custom** for customized engine configuration:<br> - **Coordinator nodes (max. 1):** Select the run rate for coordinator node (you can have a maximum of 1 node).<br> - **Worker nodes (max. 18):** Select the number of worker nodes and run rate (you can have a maximum of 18 nodes). |
    | Associated catalogs (optional) | Associate the available catalogs with the engine if necessary.  |
    {: caption="Table 1. Add engine details" caption-side="bottom"}

1. Click **Create**.
