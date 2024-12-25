---

copyright:
  years: 2022, 2024
lastupdated: "2024-12-25"

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

# Associating a catalog with an engine
{: #asso-cat-eng}

To associate a catalog or catalogs with an engine, use one of the following methods:
{: shortdesc}

- **Associating a catalog or catalogs with an engine in list view**

1. Click the overflow menu and then click **Manage associations**.

2. In **Manage associations** window, select the engine with which you want to associate the catalog or catalogs.

3. Click **Save and restart engine**.

- **Associating a catalog or catalogs with an engine in topology view**

1. Hover over the catalog that you want to associate with an engine and click the **Manage associations** icon.

2. In **Manage associations** window, select the engine with which you want to associate the catalog or catalogs.

3. Click **Save and restart engine**.

## Related API
{: #assocat_api}

For information on related API, see
* [Associate catalogs to a Presto (C++) engine](https://cloud.ibm.com/apidocs/watsonxdata#create-prestissimo-engine-catalogs)
* [Associate catalogs to Presto (Java) engine](https://cloud.ibm.com/apidocs/watsonxdata#create-presto-engine-catalogs)
* [Get Spark engine catalogs](https://cloud.ibm.com/apidocs/watsonxdata#list-spark-engine-catalogs)
* [Associate catalogs to Spark engine](https://cloud.ibm.com/apidocs/watsonxdata#create-spark-engine-catalogs)
