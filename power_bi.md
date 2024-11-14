---

copyright:
  years: 2022, 2024
lastupdated: "2024-11-14"

keywords: watsonx.data, spark, analytics, configuring
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Connecting Power BI to Presto in watsonx.data
{: #bi_intro}

This topic provides you with the procedure to connect Power BI to Presto using one of the following ODBC drivers:

*	Simba ODBC driver
*	CData ODBC driver

When you connect to the Presto engine in {{site.data.keyword.lakehouse_short}}, you can access the various connected data sources and build compelling and interactive data visualizations.


## Pre-requisites
{: #bi_preq}

*	Power BI Desktop :  Download and install the latest desktop version of Power BI using the Advanced download link. Create a Power BI account by using your email-ID and log in.
*	Based on the ODBC driver that you select, download and install one of the following:
    * Simba ODBC driver for Presto: Download and install latest desktop version of Insight software Simba ODBC driver from the [Presto ODBC Driver](https://insightsoftware.com/drivers/presto-odbc-jdbc/). Based on your computer platform (Mac or Desktop), log in to the account. After you download, you will receive a license file in registered email . Copy the file and paste it under `~\Simba Presto ODBC Driver\lib folder`.
    * CData ODBC driver for Presto: Download and install latest desktop version of CData ODBC driver for Presto from the [Presto ODBC Driver](https://www.cdata.com/drivers/presto/odbc/?kw=&cpn=18157657805&utm_source=google&utm_medium=cpc&utm_campaign=Search_-_Connector_-_Other_Drivers_-_India_+_Secondary_Countries&utm_content=All_Drivers_-_DSA&utm_term=%7C&kw=&cpn=18157657805&gad_source=1&gclid=Cj0KCQiA88a5BhDPARIsAFj595gKFdWt_8AZPuQue7BTvrPf4paiIibaqIcp1IxzBDRp3_IcGTwRGoAaAhftEALw_wcB).
*	Subscription of {{site.data.keyword.lakehouse_short}} on IBM Cloud.
*	Provision {{site.data.keyword.lakehouse_short}} instance with Presto engine.

## Authentication
{: #bi_auth}

Power BI uses Lightweight Directory Access Protocol (LDAP) authentication mechanism to connect to Presto. You need the following sign-in credentials:
*   Username: Username is `ibmlhapikey` or `ibmlhapikey_<watsonx.datauser_id>`.
*   Password: The API key of the {{site.data.keyword.lakehouse_short}} user.


## Configuring the Driver
{: #bi_config}

You can select one of the following ODBC drivers to connect to Presto from Power BI.
*	[Simba](#simba)
*	[CData](#cdata)


### Simba
{: #simba}

1. Open **ODBC Data Source** > **Run as administrator** from your computer. The **ODBC Data Source Administrator** page opens.
2. Click **System DSN**.
3. Select **Simba Presto**.
4. Click **Add**. The **Create New Data Source** page opens.
5. Select the **Simba Presto ODBC** driver for which you want to set up the data source and click **Finish**. The **Simba Presto ODBC Driver DSN Setup** page opens.
6. Provide the following details:

    - Data source name : Enter a name for your data source connection.
    - Description : Provide a description for the Presto driver setup.
    - Authentication Type : Select LDAP from the list.
    - Username : The username is `ibmlhapikey` or `ibmlhapikey_<watsonx.datauser_id>`.
    - Password : The API key of the {{site.data.keyword.lakehouse_short}} user. For more information about retrieving the API key, see [Generating the API key]({{site.data.keyword.ref-con-presto-serv-link}}).
    - Host : Hostname of the Presto engine in watsonx.data that you want to connect to. For more information about retrieving the hostname, see [Getting connection information]({{site.data.keyword.ref-get_connection-link}}).
    - Port : For information about retrieving the port number, see [Getting connection information]({{site.data.keyword.ref-get_connection-link}}).
    - Catalog : Select the Iceberg catalog (Iceberg_data) that is associated with the Presto engine in watsonx.data.
    - Schema : Select the schema that is associated with your data.

7.	Click **Test** to verify that the connection is successful. The Test results window opens to display the success message. Click **Ok**. The **Simba Presto ODBC Driver DSN Setup** page opens.
8.	Click **Ok**. The **ODBC Data Source Administrator** page opens. Click **Ok**.

### CData
{: #cdata}

1.	**Open ODBC Data Source** > **Run as administrator** from your computer. The ODBC Data Source Administrator page opens.
2.	Click **System DSN**.
3.	Select **CData Presto**.
4.	Click **Add**. The **CData ODBC Driver for Presto - DSN Configuration** page opens.
5.	Provide the following details:

    *	Data source name : Enter a name for your data source connection.
    *	Server : Hostname of the Presto engine in {{site.data.keyword.lakehouse_short}} that you want to connect to. For more information about retrieving the hostname, see [Getting connection information]({{site.data.keyword.ref-get_connection-link}}).
    *	Port : For more information about retrieving the port number, see [Getting connection information]({{site.data.keyword.ref-get_connection-link}}).
    *	Auth Scheme : Select LDAP from the list.
    *	Username : The username is `ibmlhapikey` or `ibmlhapikey_<watsonx.datauser_id>`.
    *	Password : The API key of the {{site.data.keyword.lakehouse_short}} user. For more information about retrieving the API key, see [Generating the API key]({{site.data.keyword.ref-con-presto-serv-link}}).
    *	Use SSL : Select **True** from the list.


6.	Click **Test Connection** to verify that the connection is successful. The **ODBC – DSN Configuration** window opens to display the success message. Click **Ok**. The **CData ODBC Driver for Presto - DSN Configuration** page opens.
7.	Click **Ok**. The **ODBC Data Source Administrator** page opens. Click **Ok**.

## Setting up Power BI and viewing tables
{: #bi_set}

1.	Open **Power BI Desktop**.
2.	Click **Get data from other sources**. The **Add** data to your report page opens.
3.	Click **Get data from other sources** link. The **Get Data** page opens.
4.	Search and select **ODBC**.
5.	Click **Connect**. The **From ODBC** page opens.
6.	From the **Data source name** list, select the data source that you created and click **Ok**.
7.	The **ODBC driver** page opens.
8.	Provide username and password and click **Connect**.

    Username : Username is `ibmlhapikey` or `ibmlhapikey_<watsonx.datauser_id>` and password is the API key of the {{site.data.keyword.lakehouse_short}} user. For more information about retrieving the API key, see [Generating the API key]({{site.data.keyword.ref-con-presto-serv-link}}).
9.	The **Navigator** page opens with the list of schemas in the Presto engine.
10.	Select a required table to view the preview of the table and click **Load** or **Transform Data** based on your requirement. You can build visuals by using the data.
