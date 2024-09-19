---

copyright:
  years: 2022, 2024
lastupdated: "2024-09-19"

keywords: watsonx.data, spark, analytics, configuring
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Connecting Domo to Presto in watsonx.data
{: #domo}

This topic provides you the procedure to connect Domo to Presto.

When you connect to the Presto engine in watsonx.data, you can access the various connected data sources and build compelling and interactive data visualizations.


## Pre-requisites
{: #domo_preq}


* Subscription to Domo.
* Subscription to watsonx.data on IBM Cloud.
* Provision watsonx.data instance with Presto engine.


## Authentication
{: #domo_auth}

Domo uses Lightweight Directory Access Protocol (LDAP) authentication mechanism to connect to Presto. You need the following sign-in credentials:
* Username: Username is `ibmlhapikey` or `ibmlhapikey_<watsonx.datauser_id>`.
* Password: The API key of the watosnx.data user.

## Connecting to Presto
{: #domo_prs}

1.	Log in to **Demo**.
2.	From the **Domo** home page, click **Add**.
3.	Click **Data** and from the list, select **Federated**.
4.	Click **Presto**. The **Connect a Federated DataSet** page opens.
5.	Click **ADD NEW ACCOUNT**. The **Connect a Federated DataSet** page opens. In this page, configure the Presto account and provide the following connection details:


    * Account name: Provide a name for the connection.

    * Host : Hostname of the Presto engine in watsonx.data that you want to connect to. For more information about retrieving the hostname, see [Getting connection information](watsonxdata?topic=watsonxdata-get_connection).

    * Port (optional) : For information about retrieving the port number, see [Getting connection information](watsonxdata?topic=watsonxdata-get_connection).

    * Username : Username is `ibmlhapikey` or `ibmlhapikey_<watsonx.datauser_id>`.

    *	Password : The API key of the watosnx.data user. For more information about retrieving the API key, see [Generating the API key](watsonxdata?topic=watsonxdata-con-presto-serv#get-ibmapi-key).


6.	Click **Connect**. The **Connect a Federated DataSet** page opens displaying the Presto account you created.
7.	Select the Presto account that you want to connect to and click **Connect**.
8.	The **Connect a Federated DataSet** page opens. Provide the following details:

    *	Database : The database that you want to connect to.

    *	Schema : The schema that is associated with your data.

    *	Table : The table that you want to consider for data analysis.

9.	Click **GET SCHEMA**. Click the **Schema** tab to view the list of columns in the table.
10.	Click **SELECT ALL** and click **Create**. The **Federated `<table_name>`** page opens. In this page, you can view the table data from the **DATA** tab, create visualization, share the dataset, and cleanup the data set.


## Performing data analysis
{: #domo_analys}

You can perform data federation operations and generate insights from the data to make better decisions. Here, the section describes the procedure to perform a JOIN operation between tables.

1.	The **Federated `<table_name>`** page opens. Select **Data** tab and click **Edit**. You can view the table details.
2.	Click the **DataSet** tab. You can view the table that you selected.
3.	Click **ADD JOIN**. The **Join new DataSet** page opens.
4.	Select the data sets (tables that you want to join) to perform a JOIN operation.
5.	Select the columns from the **JOIN KEYS** list.
6.	Select the type of JOIN that you want to perform and click **SELECT COLUMNS**.
7.	You can view the result in the **View Federated** `<table_name>` page.
