---

copyright:
  years: 2022, 2024
lastupdated: "2024-12-01"

keywords: lakehouse, engine, catalog, watsonx.data

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

# Dissociating a catalog from an engine
{: #disso-cat-eng}

To dissociate a catalog or catalogs from an engine, use one of the following methods:
{: shortdesc}

- **Dissociating a catalog or catalogs from an engine in list view**

1. Click the overflow menu and then click **Manage associations**.

2. In **Manage associations** window, clear the checkbox in the **Engine** column.

3. Click **Save and restart engine**.

- **Dissociating a catalog or catalogs from an engine in topology view**

1. Hover over the catalog that you want to associate with an engine and click the **Manage associations** icon.

2. In **Manage associations** window, clear the checkbox in the **Engine** column.

3. Click **Save and restart engine**.

## Related API
{: #dissocat_api}

For information on related API, see [Disassociate catalogs from a Presto (Java) engine](https://cloud.ibm.com/apidocs/watsonxdata#delete-presto-engine-catalogs), [Disassociate catalogs from a Presto (C++) engine](https://cloud.ibm.com/apidocs/watsonxdata#delete-prestissimo-engine-catalogs), [Disassociate catalogs from a Spark engine](https://cloud.ibm.com/apidocs/watsonxdata#delete-spark-engine-catalogs).
