---

copyright:
  years: 2022, 2023
lastupdated: "2023-11-29"

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

# Adding a database-catalog pair
{: #reg_database}

A database is one of the data sources that you can register and use in {{site.data.keyword.lakehouse_full}}. A catalog defines the schemas and metadata for a data source.
{: shortdesc}

When you add your own object storage bucket or database, or query the data in these data sources through the query engines of {{site.data.keyword.lakehouse_short}}, egress charges for pulling data out of these sources might apply depending on your service provider. If you are using managed services, consult your service provider's documentation or support for details about these charges.
{: important}

To reduce the latency issues, it is recommended to colocate your additional object storage buckets or databases in the region where {{site.data.keyword.lakehouse_short}} instance is provisioned.
{: important}

IBM supports the following database types:

* IBM Db2: IBM Db2 is a database that contains relational data.
* IBM Netezza: Netezza Performance Server is a platform for high-performance data warehousing and analytics.
* Apache Kafka: Apache Kafka is a distributed event streaming platform. Connect to an Apache Kafka real-time processing server to write and to read Streams of events from and into topics.
* MongoDB: IBM Cloud Databases for MongoDB is a MongoDB database that is managed by IBM Cloud. It uses a JSON document store with a rich query and aggregation framework.
* MySQL: IBM Cloud Databases for MySQL extend the capabilities of MySQL by offering an auto-scaling deployment system that is managed on IBM Cloud that delivers high availability, redundancy, and automated backups. IBM Cloud Databases for MySQL were formerly known as IBM Cloud Compose for MySQL.
* PostgreSQL: IBM Cloud Databases for PostgreSQL is an open source object-relational database that is highly customizable. It’s a feature-rich enterprise database with JSON support.
* SQL Server: Microsoft SQL Server is a relational database management system.
* Custom: Any database that you bring in.
* Teradata: Teradata is a relational database management system.
* Elasticsearch: Elastic search is a NoSQL database that stores data in an unstructured manner.
* Snowflake: Snowflake is a cloud hosted relational database for building data warehouse.
* SingleStore: SingleStore is a relational database management system designed for data-intensive applications.



To add a database-catalog pair, complete the following steps.

1. Log in to the {{site.data.keyword.lakehouse_short}} console.
2. From the navigation menu, select **Infrastructure manager**.
3. To add a database, click **Add component** and select **Add database**.
4. In the **Add database** window, select a database from the **Database type** drop-down list. The list includes the following database types:
    * IBM Db2
    * IBM Netezza
    * Apache Kafka
    * MongoDB
    * MySQL
    * PostgreSQL
    * SQL Server
    * Custom
    * Teradata
    * Elasticsearch
    * Snowflake
    * SingleStore

    You can now use the custom catalog to create connections to data stores that are not provided by the built-in connectors. For example, you can set up the custom connector that is hosted and managed by AWS Glue. For more information see, {: #custom_database}
    {: note}

5. Based on the database type selected, click the respective link to configure the database details.
    * [IBM Db2](#db2)
    * [IBM Netezza](#db2)
    * [Apache Kafka](#kafka)
    * [MongoDB](#db2)
    * [MySQL](#sql)
    * [PostgreSQL](#postgrsql)
    * [SQL Server](#postgrsql)
    * [Custom](#cust)
    * [Teradata](#singlestore)
    * [Elasticsearch](#sql)
    * [Snowflake](#snowflake)
    * [SingleStore](#singlestore)



 * **IBM Db2, MongoDB, or IBM Netezza**{: #db2}

    If you select **IBM Db2, MongoDB, or IBM Netezza** from the **Database type** drop-down list, configure the following details:

    Two databases with the same name cannot be added.
   {: note}

    | Field           | Description        |
    |------------------|--------------------|
    | Database name     | Enter the name of your database. For MongoDB, enter the name of your authentication database.|
    | Display name    | Enter the database name to be displayed on the screen. |
    | Hostname            | Enter the hostname.  |
    | Port             | Enter the port number. |
    | Username           | Enter the port username.  |
    | Password           | Enter the password.  |
    |Test connection     | Click the Test connection link to test the database connection. If the database connection is successful, a success message displays.|
    | SSL Connection   | Upload the SSL certificate to secure the database connection. To establish a secure connection, do the following steps: \n i. Select the SSL Connection checkbox. The Upload SSL certificate (pem or crt) link is enabled. \n ii. Click the Upload SSL certificate (pem or crt) link. \n iii. Browse the SSL certificate and upload.|
    | Associated catalog definition | Enter the name of the catalog. This catalog is automatically associated with your database. |
    {: caption="Table 1. Register database" caption-side="bottom"}

    You can add multiple host information for MongoDB. To add, click the **Add** icon. A new row appears for adding hostname and port. Enter the details.
    {: note}


 * **Apache Kafka**{: #kafka}

    If you select **Apache Kafka** from the **Database type** drop-down list, configure the following details:

    Two databases with the same name cannot be added.
   {: note}

    | Field           | Description        |
    |------------------|--------------------|
    | Display name    | Enter the database name to be displayed on the screen. |
    | Hostname            | Enter the hostname.  |
    | Port             | Enter the port number. |
    | Username           | Enter the port username.  |
    | Password           | Enter the password.  |
    | Topics             | Type the list of topics present in the Apache Kafka instance that you need to work with watsonx.data.|
    | SASL connection   | Enable the Simple Authentication Security Layer (SASL) to include authentication mechanism. If you enable SASL, specify the username and API key.|
    |Test connection     | Click the Test connection link to test the database connection. If the database connection is successful, a success message displays.|
    | Associated catalog definition | Enter the name of the catalog. This catalog is automatically associated with your database. |
    {: caption="Table 2. Register database" caption-side="bottom"}

    You can add multiple host information for **Apache Kafka**. To add, click the **Add** icon. A new row appears for adding hostname and port. Enter the details.
    {: note}

    * **MySQL or Elasticsearch**{: #sql}

    If you select **MySQL or Elastcisearch** from the **Database type** drop-down list, configure the following details:

    Two databases with the same name cannot be added.
   {: note}

    | Field           | Description        |
    |------------------|--------------------|
    | Display name    | Enter the database name to be displayed on the screen. |
    | Hostname            | Enter the hostname.  |
    | Port             | Enter the port number. |
    | Username           | Enter the port username.  |
    | Password           | Enter the password.  |
    | SSL Connection   | Upload the SSL certificate to secure the database connection. To establish a secure connection, do the following steps: \n i. Select the SSL Connection checkbox. The Upload SSL certificate (pem or crt) link is enabled. \n ii. Click the Upload SSL certificate (pem or crt) link. \n iii. Browse the SSL certificate and upload.|
    |Test connection     | Click the Test connection link to test the database connection. If the database connection is successful, a success message displays.|
    | Associated catalog definition | Enter the name of the catalog. This catalog is automatically associated with your database. |
    {: caption="Table 3. Register database" caption-side="bottom"}

 * **PostgreSQL or SQL Server**{: #postgrsql}

    If you select **PostgreSQL or SQL Server** from the **Database type** drop-down list, configure the following details:

    Two databases with the same name cannot be added.
   {: note}

    | Field           | Description        |
    |------------------|--------------------|
    | Database name     | Enter the name of your database.|
    | Display name    | Enter the database name to be displayed on the screen. |
    | Hostname            | Enter the hostname.  |
    | Port             | Enter the port number. |
    | Username           | Enter the port username.  |
    | Password           | Enter the password.  |
    |Test connection     | Click the Test connection link to test the database connection. If the database connection is successful, a success message displays.|
    | Associated catalog definition | Enter the name of the catalog. This catalog is automatically associated with your database. |
    {: caption="Table 4. Register database" caption-side="bottom"}


 * **Custom**{: #cust}

    If you select **Custom** from the **Database type** drop-down list, configure the following details:

    Two databases with the same name cannot be added.
   {: note}

   For more information, see

    | Field           | Description        |
    |------------------|--------------------|
    | Display name    | Enter the database name to be displayed on the screen. |
    | connector.name     | Enter the name of the database connector that you want to add.  |
    | Property value             | Enter the properties (and their values) to be configured for the database. |
    | Port           | Enter the port number.  |
    | Encryption           | Enable if you want to include encryption.  |
    | Associated catalog definition | Enter the name of the catalog. This catalog is automatically associated with your database. |
    {: caption="Table 5. Register database" caption-side="bottom"}

 * **SingleStore or Teradata**{: #singlestore}

    If you select **SingleStore or Teradata** from the **Database type** drop-down list, configure the following details:

    Two databases with the same name cannot be added.
   {: note}

    | Field           | Description        |
    |------------------|--------------------|
    | Database name     | Enter the name of your database.|
    | Display name    | Enter the database name to be displayed on the screen. |
    | Hostname            | Enter the hostname.  |
    | Port             | Enter the port number. |
    | Username           | Enter the port username.  |
    | Password           | Enter the password.  |
    |SSL Connection     | Upload the SSL certificate to secure the database connection. To establish a secure connection, do the following steps: \n i. Select the SSL Connection checkbox. The Upload SSL certificate (pem or crt) link is enabled. \n ii. Click the Upload SSL certificate (pem or crt) link. \n iii. Browse the SSL certificate and upload.|
    | Associated catalog definition | Enter the name of the catalog. This catalog is automatically associated with your database. |
    {: caption="Table 6. Register database" caption-side="bottom"}

 * **Snowflake**{: #snowflake}

    If you select **Snowflake** from the **Database type** drop-down list, configure the following details:

    Two databases with the same name cannot be added.
   {: note}

    | Field           | Description        |
    |------------------|--------------------|
    | Database name     | Enter the name of your database.|
    | Display name    | Enter the database name to be displayed on the screen. |
    | Hostname            | Enter the hostname.  |
    | Username           | Enter the port username.  |
    | Password           | Enter the password.  |
    | Associated catalog definition | Enter the name of the catalog. This catalog is automatically associated with your database. |
    {: caption="Table 7. Register database" caption-side="bottom"}

6. Click **Add**.
