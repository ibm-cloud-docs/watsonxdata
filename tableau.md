---

copyright:
  years: 2022, 2024
lastupdated: "2024-11-13"

keywords: watsonx.data, spark, analytics, configuring
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Connecting Tableau to Presto in watsonx.data
{: #tableau}

This topic provides you with the procedure to connect Tableau to Presto.

When you connect to the Presto engine in watsonx.data, you can access the various connected data sources and build compelling and interactive data visualizations.


## Pre-requisites
{: #tableau_preq}


* Tableau desktop: Download and install the latest desktop version of Tableau on your computer.
* Subscription to watsonx.data on IBM Cloud.
* Provision watsonx.data instance with Presto engine.
* Download the Presto JDBC driver from [JDBC Driver](https://prestodb.io/docs/current/installation/jdbc.html). After you download the Presto JDBC driver, add it to the path `/Library/Tableau/Drivers` where Tableau is installed.

## Authentication
{: #tableau_auth}

Tableau uses Lightweight Directory Access Protocol (LDAP) authentication mechanism to connect to Presto. You need the following sign-in credentials:
* Username: Username is `ibmlhapikey` or `ibmlhapikey_<watsonx.datauser_id>`.
* Password: The API key of the watosnx.data user.

## Connecting to Presto
{: #tableau_prs}


1.	Open **Tableau desktop**.
2.	Click **More** and select **Presto**. The **Presto** window opens.
3.	In the **General** tab, provide the following details:

    * Server : Hostname of the Presto engine in watsonx.data that you want to connect to. For more information about retrieving the hostname, see [Getting connection information]({{site.data.keyword.ref-get_connection-link}}).
    * Port : For more information about retrieving the port number, see [Getting connection information]({{site.data.keyword.ref-get_connection-link}}).
    * Catalog : Enter the Iceberg catalog that is associated with the Presto engine in watsonx.data.
    * Schema (Optional) : Enter the name of the schema that is associated with your data.
    * Authentication : Select LDAP from the list.
    * Username : The username is `ibmlhapikey` or `ibmlhapikey_<watsonx.datauser_id>`. For example, `ibmlhapikey_joe@ibm.com`.
    * Password : The API key of the watosnx.data user. For more information about retrieving the API key, see [Generating the API key]({{site.data.keyword.ref-con-presto-serv-link}}).


4.	In the **Initial SQL** tab (Optional), specify the initial SQL query that you want to run when a connection is made to Presto.
5.	Click **Sign In**. The **Data Source** page opens when connection is successful.

## Performing data analysis
{: #tableau_analys}

1.	From the **Data Source** page, you can view the Iceberg catalog.
2.	Select a schema from the **Schema** drop-down list.
3.	Select a table from the **Tables** field.
4.	Drag the table to create the data model.

For more information, see [Connect to a Custom SQL Query](https://help.tableau.com/current/pro/desktop/en-us/customsql.htm).
