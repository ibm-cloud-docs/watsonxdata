---

copyright:
  years: 2022, 2024
lastupdated: "2025-02-19"

keywords: lakehouse, database, watsonx.data

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


# Custom
{: #custom_database}

You can now use the Custom data source to create data sources that are not provided by the built-in connectors. Custom data source can be used for connectors that are supported by Presto as in the Presto documentation but not listed in IBM {{site.data.keyword.lakehouse_full}} supported connectors or data sources. This feature is applicable for Presto (Java) and Presto (C++) engines. For Presto (C++) engine, only Hive, Apache Iceberg, Arrow Flight service, and Custom data sources can be associated.
{: shortdesc}


To add a custom data source, complete the following steps.

1. Log in to the {{site.data.keyword.lakehouse_short}} console.
2. From the navigation menu, select **Infrastructure manager**.
3. To define and connect a data source, click **Add component**.
4. In the **Data sources** section, select **Custom data source**.
5. Configure the following details:


    Use of this feature may crash your engine if configured incorrectly. IBM does not provide support for use of this feature.
   {: note}

    Custom databases do not support SSL configuration.
   {: note}



    | Field           | Description        |
    |------------------|--------------------|
    | Display name    | Enter the database name to be displayed on the screen. |
    | Property value             | Enter the properties and their values to be configured for the database. Enter the property name:value pair as specified in Presto documentation. You can add multiple properties.|
    | connector.name=     | Enter the name of the database connector that you want to add as specified in the Presto documentation.  |
    | Encryption           | Encrypting values of the keys are stored.  |
    | Associated catalog | Select the checkbox to associate a catalog to the data source. This catalog is automatically associated with your data source and serves as your query interface with the data stored within. |
    | Catalog name | Enter the name of the catalog. |
    | Create |  Click Create to create the data source.|
    {: caption="Register data source" caption-side="bottom"}

You can use the Custom data source for the following connectors in IBM watsonx.data for Presto engine:

* Local File connector: The Local File connector is used to display the http request logs of a worker. Use the custom data source option with the following properties. For more information, see [Local File connector](https://prestodb.io/docs/current/connector/localfile.html).

   * connector.name=localfile
   * presto-logs.http-request-log.location=var/log
   * presto-logs.http-request-log.pattern=http-request.log*

* Black Hole connector: The Black Hole connector is designed for high-performance testing of other components. Use the custom data source option with the following property. For more information, see [Black Hole connector](https://prestodb.io/docs/current/connector/blackhole.html).

   * connector.name=blackhole
