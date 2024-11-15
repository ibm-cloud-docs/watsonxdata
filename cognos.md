---

copyright:
  years: 2022, 2024
lastupdated: "2024-11-14"

keywords: watsonx.data, spark, analytics, configuring
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Connecting IBM Cognos Analytics to Presto in watsonx.data
{: #cognos}

This topic provides you with the procedure to connect IBM Cognos Analytics to Presto. IBM Cognos Analytics provides AI-powered automation capabilities and allows you to generate insights from the connected data sources.

## Before you begin
{: #cognos_preq}

### Pre-requisites for IBM Cognos Analytics
{: #cognos_req}

   * IBM Cognos Analytics version 12.0.1 or above.
   * Download the Presto JDBC driver from [JDBC Drivers](https://prestodb.io/docs/current/installation/jdbc.html). Use a version of the JDBC driver, which is supported by IBM Cognos Analytics. Copy the driver to IBM Cognos Analytics installation_location\drivers directory, and restart the query service.
   * Data source Connections administrator privilege to create data server connections.

### Pre-requisites for IBM watsonx.data
{: #pres_req}

   * Subscription to watsonx.data on IBM Cloud.
   * Provision watsonx.data instance with Presto engine.

## Connecting to Presto
{: #cognos_prs}


1. Log in to **{{site.data.keyword.cognosanalytics_short}}**.
1. From the navigation menu, click **New**.
1. Click **Data server**. The **Create data server connection** page opens. In this page, do the following:

   1. Provide the following details:

      * Name: Provide a name for the connection.
      * Connection type: Select `watsonx.data`.

   2. Click **Next**.

   1. Provide the following details:

      * JDBC URL: Presto JDBC URL. For more information about retrieving the hostname and port, see [Getting connection information](watsonxdata?topic=watsonxdata-get_connection). Example of the URL : `jdbc:presto://xxxxx-xxxx-xxx-xxx-xxxxx.xxxxx.xx.x.appdomain.cloud:xxxx?SSL=true`.
      * Driver class name (optional)
      * Connection properties (optional)
      * Authentication > Method: Select **Use signon**.
      * Click **Add signon**. The **User ID and password** window opens.

   1. In the **User ID and password** window, provide the following details of the Presto engine:
      * Username : Username is `ibmlhapikey_<watsonx.datauser_id>` or `ibmlhapikey_ServiceId-<service_id>`. For example, `ibmlhapikey_joe@ibm.com` or `ibmlhapikey_ServiceId-xxxxxxx-9-9e71-xxxx-yxay-cxaraa68`.To get the `<service_id>`, see [Creating a service ID by using the console](https://ondeck.console.cloud.ibm.com/docs/account?topic=account-serviceids&interface=ui#create_serviceid).


      *	Password : The API key of the {{site.data.keyword.lakehouse_short}} user. For more information about retrieving the API key, see [Generating the API key](watsonxdata?topic=watsonxdata-con-presto-serv#get-ibmapi-key).

   1. Click **Done**.
   7. Click **Test connection** to verify that the connection is successful.
   8.	You can click **Next** when your test connection is successful.
   9. Specify the commands that the database executes when certain events occur (Optional). For more information, see [Creating a data server connection](https://www.ibm.com/docs/en/cognos-analytics/12.0.0?topic=servers-creating-data-server-connection).
   10. Click **Create**. Click **Load** to configure the assets used by the connection. The catalogs from {{site.data.keyword.lakehouse_short}} gets listed.
   11. Select the assets that you want to use in  IBM Cognos Analytics and click the **Load** link against the asset. It will load the tables present in the catalogs.
   12. Click **Done**. The **Data server connections** page opens and the connection is listed.

1. Click the watsonx.data connection that you created.
1. Click the overflow menu against the connection name. Select **Assets** to list all the available schemas and tables from the {{site.data.keyword.lakehouse_short}} instance.
1. The **Assets** page opens. Select the assets (tables and schemas) to import to {{site.data.keyword.cognosanalytics_short}}.
1. Select the table (any additional) that you want to work with and click the overflow menu against it. Click **Load metadata**. The status displays `Loaded` when the table is completely loaded.

   You can start working with the data.


1. You can also verify whether the data in the table is completely loaded. To do that:
   1. Go to Navigation menu.
   1. Click **New** > **Data module**.
   1. Select **Data Servers**.
   1. Select the {{site.data.keyword.lakehouse_short}} connection that you created.
   1. Click **OK**. View the **Data module** page with data from {{site.data.keyword.lakehouse_short}}.
