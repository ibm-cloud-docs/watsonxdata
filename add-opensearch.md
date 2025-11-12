---

copyright:
  years: 2022, 2025
lastupdated: "2025-11-12"

keywords: lakehouse, opensearch, watsonx.data

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

# Adding an OpenSearch service (Public preview)
{: #add-opensearch}

OpenSearch is an open source search and analytics engine that is designed to help you explore, analyze, and visualize large volumes of data in real time. It is built for use cases like log analytics, full-text search, application monitoring, and security event analysis.
{: shortdesc}

Complete the following steps to add an OpenSearch service:

1. Log in to the {{site.data.keyword.lakehouse_short}} console.
2. From the navigation menu, select **Infrastructure Manager**.
3. To define and connect to a service, click **Add component**, select **OpenSearch**, and click **Next**.
4. In the **Add component - OpenSearch** window, provide the following details.
   * Select the service. For example, **OpenSearch**.
   * Select the suitable size. For example, **Starter, which includes one coordinator node and 1 worker node.
6. Click **Create**.
The OpenSearch service is created and displayed in the **Infrastructure Manager** page.
You can create only one OpenSearch service in an instance and only instance administrators are authorized to do all the OpenSearch operations.
{: note}
