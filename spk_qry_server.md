---

copyright:
  years: 2022, 2025
lastupdated: "2025-06-05"

keywords: query, server, spark

subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Managing Spark query server
{: #spk_qry_srver}


Spark query server is a server that allows you to establish connection with tools such as Data Build Tool (dbt) integration and DBBeaver. You can start a Spark query server to integrate with  Data Build Tool (dbt) integration and DBBeaver to query and analyze your data.
{: .shortdesc}

**Applies to** : [Spark engine]{: tag-blue}  [Gluten accelerated Spark engine]{: tag-green}

## Before you begin
{: #spk_qry_srver_bfb}

* Install watsonx.data.
* Provision native Spark engine in watsonx.data.

## Create a Spark query server
{: #crt_spk_qry_srver}

For the Spark engine to integrate with dbt tool and work as a query engine, you must create a Spark query server.

1. Log in to the watsonx.data instance.
1. Navigate to **Infrastructure manager**. Click the Spark engine.
1. Click **Query servers** tab.
1. Click **Create query servers**. The **Create query servers** page opens.
1. Provide the following details:
    * Name: Enter a name for the query server that you create.
    * Driver and Executor cores and memory.
    * Username: The watsonx.data login username.
    * API key: Your API key. To generate an API key, see [Managing user API keys](https://cloud.ibm.com/docs/account?topic=account-userapikey&interface=ui#manage-user-keys).

1. Click **Create**. The query server is created and will be in ACCEPTED status. You can start using the server when the status becomes ACTIVE.

You can view the query server details like, the name, ID, status, server start time and stop time, and the connection URL.
{: note}

## Retrieve the query server connection details
{: #ret_con_dtls}

To configure the profile file in dbt tool, you must save the query server connection details. See [Retrieve the query server connection details]().

1. From the **Query servers** tab, select the query server that is in ACTIVE state.
1. Click the overflow menu against the query server that you select.
1. Click **View connection details**. The Connection details page opens with the profile configuration.
1. Copy the connection details.
1. Paste the connection details in the `profiles.yml` file that is located in .dbt of your home directory.

   Alternatively, you can retrieve the connection details from the Connection information page. From the navigation menu, go to ConfigurationsConnection informationData Build Tool (DBT). For more information, see Data Build Tool.
   {: note}

## Viewing the Spark query server

## Stopping the Spark query server

## Integrations supported by the spark query server


* Using **Data Build Tool (dbt)** : To work with dbt, see db integration.
* Integration using DBeaver (JDBC clients) : See Connecting to Spark query server by using Spark JDBC Driver.
* Using Java (JDBC Client): See Connecting to Spark query server by using Spark JDBC Driver.
* Using Python (PyHive JDBC Client): See Connecting to Spark query server by using Spark JDBC Driver.
