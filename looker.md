---

copyright:
  years: 2022, 2024
lastupdated: "2024-09-19"

keywords: watsonx.data, spark, analytics, configuring
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Connecting Looker to Presto in watsonx.data
{: #looker}

This topic provides you with the procedure to connect Looker to Presto.

When you connect to the Presto engine in watsonx.data, you can access the various connected data sources and build compelling and interactive data visualizations.


## Pre-requisites
{: #looker_preq}


* Subscription to Looker.
* Subscription to watsonx.data on IBM Cloud.
* Provision watsonx.data instance with Presto engine.


## Authentication
{: #looker_auth}

Looker uses Lightweight Directory Access Protocol (LDAP) authentication mechanism to connect to Presto. It uses the following sign-in credentials:
* Username: Username is `ibmlhapikey` or `ibmlhapikey_<watsonx.datauser_id>`.
* Password: The API key of the watosnx.data user.

## Connecting to Presto
{: #looker_prs}

1. Log in to **Looker**.
2. From the **LookerML Projects** page, click **Configure New Model**. The **Configure a Model** page opens.
3. Configure the following details:

    * Model : Enter the model name for the project.
    * Project : Enter a project name. A project is a collection of LookML files that describe how Presto tables are related to each other.
    * Allowed Connections : Select `All`.

4.	Click **Save**. The project gets listed under the **Pending Projects** section.
5.	Click the **Configure** button against the project and select **Allowed Connections** as `All`.
6.	Go to **Looker** > **Admin**.
7.	Select **Connections** from the **Database** list.
8.	Click **Add Connection**. The **Connect your database to the Looker** page opens.
9.	Provide a name for the connection and the Looker project name.
10.	From the **Dialect** list, select **PrestoDB** and provide the following Presto details from watsonx.data.

    * Server : Hostname of the Presto engine in watsonx.data that you want to connect to. For more information about retrieving the hostname, see [Getting connection information](watsonxdata?topic=watsonxdata-get_connection).
    * Port : The Presto port that Looker should use to connect to. For more information about retrieving the port number, see [Getting connection information](watsonxdata?topic=watsonxdata-get_connection).
    * Database : The name of the database in watsonx.data.
    * Schema (Optional) : Enter the name of the schema that is associated with your data.
    * Username: The username is `ibmlhapikey` or `ibmlhapikey_<watsonx.datauser_id>`.
    * Password : The API key of the watosnx.data user. For more information about retrieving the API key, see [Generating the API key](watsonxdata?topic=watsonxdata-con-presto-serv#get-ibmapi-key).
    * Optional settings : For more information about the optional settings, see [Optional settings](https://cloud.google.com/looker/docs/connecting-to-your-db#optional_settings).


11.	Click **Test** to verify that the connection is successful.
12.	You can click **Connect** when your test connection is successful. A success message is displayed on top of the page.
13.	Click **Test** against the connection. The following options are listed:

    * Can connect
    * Can cancel queries
    * (optional) Can check database presto version (0.286)



## Performing data analysis
{: #looker_analys}

After you establish a connection with Presto, you can execute query and generate insights.

1.	Go to **Looker** > **Develop**.
2.	Click **SQL Runner**.
3.	From the **SQL Runner** page, select **Database** tab.
4.	Select the **Schema** and **Table** from which you need to analyse the data.
5.	In the **SQL QUERY** section, write a query and click **Run**. The following is a sample query.

    SELECT * FROM SCHEMA_NAME.TABLE_NAME LIMIT 10

You can view the result in the **RESULTS** section.

For more information on data analysis, see [Data analysis](https://cloud.google.com/looker/docs/connecting-to-your-db).
