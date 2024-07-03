---

copyright:
  years: 2017, 2024
lastupdated: "2024-07-03"

keywords: watsonx.data, spark, emr
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Provisioning a Presto (C++) engine
{: #pcpp_prov}

You can provision a Presto (C++) engine in {{site.data.keyword.lakehouse_short}} to run SQL queries on your data source and fetch the queried data.

## Procedure
{: #pcpp_prov_pros}

1. Log in to the {{site.data.keyword.lakehouse_short}} console.
1. From the navigation menu, select **Infrastructure Manager**.
1. To provision an engine, click **Add component** and select **Add engine**.
1. In the **Add engine** window, provide the following details to sign up new compute to work with your data:

    | Field | Description |
    | --- | --- |
    | Type | Select the engine type (`Presto (C++) v0.286`) from the list. |
    | Display name | Enter your compute engine name. |
    | Size | Select the engine size. **Custom** size includes 1 coordinator node and 3 worker nodes. |
    | Associated catalogs (optional) | Associate the available catalogs (`hive_data`) with the engine if necessary. |
    {: caption="Table 1. Add engine details" caption-side="bottom"}

1. Click **Provision**.
