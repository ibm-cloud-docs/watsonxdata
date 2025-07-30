---

copyright:
  years: 2022, 2025
lastupdated: "2025-07-30"

keywords: watsonx.data, ripasso, watsonx BI
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Connecting to watsonx BI
{: #wxbi_intro}

The topic details the procedure to connect watsonx BI to Presto. The connection makes it easy for data scientists and data analysts to interact with the data in various connected data sources and derive insights from the data available in {{site.data.keyword.lakehouse_short}}. IBM watsonx BI allows you to query and understand the data in a user friendly manner.

## Pre-requisites
{: #wxbi_preq}

* Subscription to {{site.data.keyword.lakehouse_short}} on IBM Cloud. Provision {{site.data.keyword.lakehouse_short}} instance.
* Subscription to watsonx BI on IBM Cloud. Provision watsonx BI instance (any plan).

## Procedure
{: #wxbi_proc}


1. Log in to {{site.data.keyword.lakehouse_short}} instance.
2. From the navigation menu, select **Configurations**.
3. Click the **watsonx BI** tile.
4. If you already have the subscription of **IBM watsonx BI**, click **Launch watsonx BI** to launch the welcome page of **IBM watsonx BI**. Else, you are redirected to the **IBM Cloud Catalog** page. [Provision **IBM watsonx BI** instance](https://cloud.ibm.com/docs/allowlist/watsonx-bi?topic=watsonx-bi-getting-started) and try again.
5. From the **IBM watsonx BI** welcome page, do the following setup:

   a. Click **Start setup**.

   b. Select the Cloud Object Storage that you want to use. The storages available in your {{site.data.keyword.lakehouse_short}} instance are listed here.

   c. Click **Next**. Select the language model that you want to use.

   d. Click **Next**. Choose the sample data or **Skip** the step if you do not want to add a sample data.

   e. Click **Add members** to invite others to join the account and explore watsonx BI. The **Configuration and settings** page opens. Click **Add members**. You can add users or groups. Search and add users or groups.

     You can also do this later.
     {: note}

6. Go to the **Home** page. The watsonx BI prompt window opens. You can start asking questions to retrieve insights from the data.



For more information about connecting from watsonx BI, see [Connecting to watsonx.data from watsonx BI](https://cloud.ibm.com/docs/allowlist/watsonx-bi?topic=watsonx-bi-wxd).
