---

copyright:
  years: 2022, 2024
lastupdated: "2024-08-01"

keywords: connection, watsonx.data

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

# Getting connection information
{: #get_connection}

You can now find the connectivity information for {{site.data.keyword.lakehouse_full}} in the **Connection information** tile in the **Configurations** page and in the **Instance details** page. You can copy JSON snippet and export JSON. This information is useful to create connections between IBM Cloud Pak for Data and {{site.data.keyword.lakehouse_short}}.

1. The **Connection information** tile in the **Configurations** page provides the following information:

   * **Instance details**:
   * Host IP address
   * Port
   * Instance CRN
   * SSL certificate
   * **Engine and service connection details**
   * Select the checkbox for **Generate JSON for IBM Cloud Pak for Data and watsonx** if you are connecting to {{site.data.keyword.lakehouse_full}} from IBM Cloud Pak for Data or from watsonx.ai.
   * You can select one engine for the JSON snippet.
2. The **Instance details** page provides the following details. To open the Instance details, click the i icon on the home page.

   * Region
   * Plan type
   * Cloud resource name (CRN)
   * Instance ID
   * Data Access Service (DAS) endpoint
   * Common Policy Gateway (CPG) endpoint

## Data Build Tool (DBT)
{: #get_connection_dbt}

From the **Data Build Tool (DBT)** tab you can view the following details:

### Spark engines
{: #get_connection_dbt_spk}

Expand your Spark engine to see the following details:

* Spark engine endpoint
* Application endpoint
* Port

### Associated query servers
{: #get_connection_dbt_qs}

Expand the associated query server to view the following details:

* Hostname
* URI
* Catalog: You can change the catalog by clicking the pencil icon.
* Instance CRN
* Username
* API key: Enter your platform API key here. For information about generating platform API key, see [Creating an API key in the console](https://cloud.ibm.com/docs/account?topic=account-userapikey&interface=ui#create_user_key).

You can copy the profile details by clicking **Copy profile snippet** or export the details as a yaml file by clicking **Export profile snippet**.
