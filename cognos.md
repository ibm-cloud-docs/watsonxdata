---

copyright:
  years: 2022, 2024
lastupdated: "2024-10-08"

keywords: watsonx.data, spark, analytics, configuring
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Connecting Cognos to Presto in watsonx.data
{: #cognos}

This topic provides you with the procedure to connect Cognos to Presto.

When you connect to the Presto engine in watsonx.data, Cognos Analytics provides AI-powered automation and insights from the connected data sources.



## Pre-requisites
{: #cognos_preq}


* Cognos Analytics: Download and install the latest desktop version of Cognos on your computer.
* Most data server connections require a database vendor-supplied JDBC driver. Use a version of the JDBC driver that is compatible with Java™ Runtime Environment version 8. Copy the driver to the Cognos® Analytics installation_location\drivers directory, and restart the query service. Restarting the full IBM Cognos service is not necessary.
* You must have Data source Connections administrator privilege to create data server connections.
* Subscription to watsonx.data on IBM Cloud.
* Provision watsonx.data instance with Presto engine.

## Authentication
{: #cognos_auth}

Tableau uses Lightweight Directory Access Protocol (LDAP) authentication mechanism to connect to Presto. You need the following sign-in credentials:
* Username: Username is `ibmlhapikey` or `ibmlhapikey_<watsonx.datauser_id>`.
* Password: The API key of the watosnx.data user.

## Connecting to Presto
{: #cognos_prs}


1. Log in to **{{site.data.keyword.cognosanalytics_short}}**.
1. From the navigation menu, select **Manage**.
1. Click **Data server connections**. The **Data server connections** page opens.
1. Click **New** > **Add data server**. The **Create data server connection** page opens. In this page, do the following:

   1. Provide the following details:

      * Name: Provide a name for the connection.
      * Connection type: Select `watsonx.data`.

   2. Click **Next**.

   1. Provide the following details:

      * JDBC URL: Presto JDBC URL. For more information about retrieving the hostname, see [Getting connection information](watsonxdata?topic=watsonxdata-get_connection).
      * Driver class name (optional): Select `watsonx.data`.
      * Connection properties (optional):
      * Authentication > Method: Select **Use signon**.

   1. In the **User ID and password** window, provide the following details:
      * Username : Username is `ibmlhapikey` or `ibmlhapikey_<watsonx.datauser_id>`.

      *	Password : The API key of the watosnx.data user. For more information about retrieving the API key, see [Generating the API key](watsonxdata?topic=watsonxdata-con-presto-serv#get-ibmapi-key).

   1. Clcik **Done**.
   7.	Click **Test connection** to verify that the connection is successful.
   8.	You can click **Next** when your test connection is successful and create the connection.

1. Go to the **Data server connections** page. Click the watsonx.data connection that you created.
1. Click the overflow menu against the connection name. Select **Assets** to list all the available schemas and tables from the {{site.data.keyword.lakehouse_short}} instance.
1. The **Assets** page opens. Select the assets (tables and schemas) to import to {{site.data.keyword.cognosanalytics_short}}.
1. Select the table that you want to work with and click the overflow menu against it. Click **Load metadata**. The status displays `Loaded` when the table is completely loaded.

   You can start working with the data.

1. You can also verify whether the data in the table is completely loaded. To do that:
   1. Go to Navigation menu.
   1. Click **New** > **Data module**.
   1. Select **Data Servers**.
   1. Select the {{site.data.keyword.lakehouse_short}} connection that you created.
   1. Click **OK**. View the **Data module** page with data from {{site.data.keyword.lakehouse_short}}.
