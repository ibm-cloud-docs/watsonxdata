---

copyright:
  years: 2022, 2024
lastupdated: "2024-09-19"

keywords: watsonx.data, spark, analytics, configuring
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Connecting Qlik to Presto in watsonx.data
{: #qlik}

This topic provides you the procedure to connect Qlik to Presto.

When you connect to the Presto engine in watsonx.data, you can access the various connected data sources and perform data integration and analytics solutions that support your AI strategy.


## Pre-requisites
{: #qlik_preq}


* Subscription to Qlik.
* Subscription to watsonx.data on IBM Cloud.
* Provision watsonx.data instance with Presto engine.


## Authentication
{: #qlik_auth}

Qlik uses Lightweight Directory Access Protocol (LDAP) authentication mechanism to connect to Presto. You need the following sign-in credentials:
* Username: Username is `ibmlhapikey` or `ibmlhapikey_<watsonx.datauser_id>`.
* Password: The API key of the watosnx.data user.

## Connecting to Presto
{: #qlik_prs}


1.	Log in to **Qlik**.
2.	From the **Home** page, click **Create** > **Analytics App**. The **Create a new app** page opens.
3.	Provide a name for the integration and click **Create**.
4.	To add data to the app, click **Files** and other sources.
5.	Search for Presto in the **Connect** to a new data source section.
6.	In the **Create new connection (Presto)** window, provide the following details:

    *	Server : Hostname of the Presto engine in watsonx.data that you want to connect to. For more information about retrieving the hostname, see [Getting connection information](watsonxdata?topic=watsonxdata-get_connection).
    *	Port : For information about retrieving the port number, see [Getting connection information](watsonxdata?topic=watsonxdata-get_connection).
    *	Catalogue : Enter the Iceberg catalog that is associated with the Presto engine in watsonx.data.
    *	Schema (Optional) : Enter the name of the schema that is associated with your data.
    *	Authentication : Select LDAP from the list.
    *	Username : The username is `ibmlhapikey` or `ibmlhapikey_<watsonx.datauser_id>`.
    *	Password : The API key of the watosnx.data user. For more information about retrieving the API key, see [Generating the API key](watsonxdata?topic=watsonxdata-con-presto-serv#get-ibmapi-key).

7.	Click **Test connection** to verify that the connection is successful.
8.	You can click **Create** when your test connection is successful. The Data Source page opens when connection is successful.

## Performing data analysis
{: #qlik_analys}

1.	In the **Data Source** page,  from the **Database** list, select the catalog.
2.	Select the schema from the **Owner** field. The tables are listed.
3.	Select the required table and click **Preview**.
4.	Click **Next**. The **Catalog** page opens. The page lists the tables available in the schema.
5.	Select the required `<Tablename>` tile. The `<Tablename>` page opens with the table details. You can view the table details and can perform data integration and analytics.
