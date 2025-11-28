---

copyright:
  years: 2022, 2025
lastupdated: "2025-11-28"

keywords: query, server, spark

subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Managing Spark query server
{: #spk_qry_srver}

**Applies to** : [Spark engine]{: tag-blue}


Spark query server allows you to start Spark Hive based thrift server that provides the interface to collect, store, query and analyse all your lakehouse data from Spark engine.
{: .shortdesc}

Spark query server functionality can be leveraged in various ways, see [Integration](#int-spk).

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
    * You need to provide the following information when using version 2.3 or later of {{site.data.keyword.lakehouse_short}}.

       Select the **Capacity type**. You can select **Dedicated** (if configured) or **On-demand**. Choose the capacity from the list and specify the CPU cores and memory details for driver and executor.

    * Driver and Executor cores and memory. Specify this field if you are using a version earlier than 2.3 of {{site.data.keyword.lakehouse_short}}.
    * Username: The watsonx.data login username.
    * API key: Your API key. To generate an API key, see [Generating the API key](https://test.cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-con-presto-serv).
    * Specify the configuration and environment variables and the values.

1. Click **Create**. The query server is created and will be in ACCEPTED status. You can start using the server when the status becomes ACTIVE.

You can view the query server details like, the name, ID, status, server start time and stop time, and the connection URL.
{: note}

## Retrieve the query server connection details
{: #ret_con_dtls}

To configure the profile file in dbt tool, you must save the query server connection details.

1. From the **Query servers** tab, select the query server that is in ACTIVE state.
1. Click the overflow menu against the query server that you select.
1. Click **View connection details**. The Connection details page opens with the profile configuration.
1. Copy the connection details.

   Alternatively, you can retrieve the connection details from the Connection information page. From the navigation menu, go to ConfigurationsConnection informationData Build Tool (DBT).
   {: note}



## Stopping the Spark query server
{: #stp-spk}

1. From the Query servers tab, you can view the lat of query servers.
1. Click the overflow menu against the query server that you select.
1. Click **Stop**.


## Integrations supported
{: #int-spk}


* Using **Data Build Tool (dbt)** : To work with dbt, see [dbt integration](/docs/watsonxdata?topic=watsonxdata-dbt_watsonx_spark_inst).
* Integration using DBeaver (JDBC clients) : See [Connecting to Spark query server by using Spark JDBC Driver](/docs/watsonxdata?topic=watsonxdata-dbt_watsonx_connt).
* Using Java (JDBC Client): See [Connecting to Spark query server by using Spark JDBC Driver](/docs/watsonxdata?topic=watsonxdata-dbt_watsonx_connt).
* Using Python (PyHive JDBC Client): See [Connecting to Spark query server by using Spark JDBC Driver](/docs/watsonxdata?topic=watsonxdata-dbt_watsonx_connt).
