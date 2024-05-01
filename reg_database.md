---

copyright:
  years: 2022, 2024
lastupdated: "2024-04-30"

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
* Teradata: Teradata is a relational database management system.
* Elasticsearch: Elastic search is a NoSQL database that stores data in an unstructured manner.
* Snowflake: Snowflake is a cloud hosted relational database for building data warehouse.
* SingleStore: SingleStore is a relational database management system designed for data-intensive applications.
* IBM Data Virtualization Manager for z/OS: IBM Data Virtualization Manager for z/OS provides virtual, integrated views of data residing on IBM Z. It enables users and applications to have read or write access to IBM Z data in place, without having to move, replicate, or transform the data.
* Amazon Redshift: Amazon Redshift uses SQL to analyze structured and semi-structured data across data warehouses, operational databases, and data lakes. It uses AWS-designed hardware and machine learning to deliver the best price performance at any scale.
* Informix: Informix is an enterprise class Object Relational Database Management System (ORDBMS). It is extensible and provides extreme transaction performance and features to support both OLTP and Data Warehouse database services.
* Oracle: Oracle allows querying and creating tables in an external Oracle database.
* Prometheus: Prometheus allows reading Prometheus metrics as tables in Trino by using the Prometheus HTTP API mechanism.
* Custom: You can now use the custom database feature for databases that Presto supports but are not listed in {{site.data.keyword.lakehouse_short}} supported databases.


To add a database-catalog pair, complete the following steps.

1. Log in to the {{site.data.keyword.lakehouse_short}} console.
2. From the navigation menu, select **Infrastructure manager**.
3. To add a database, click **Add component** and select **Add database**.
4. In the **Add database** window, select a database from the **Database type** drop-down list. The list includes the following database types:
    * [IBM Db2](#db2)
    * [IBM Netezza](#netezza)
    * [Apache Kafka](#kafka)
    * [MongoDB](#mongo)
    * [MySQL](#mysql)
    * [PostgreSQL](#postgresql)
    * [SQL Server](#sql)
    * [Teradata](#teradata)
    * [Elasticsearch](#elastic)
    * [Snowflake](#snowflake)
    * [SingleStore](#singlestore)
    * [IBM Data Virtualization Manager for z/OS](#dvm)
    * [Amazon Redshift](#amazon)
    * [Informix](#informix)
    * [Oracle](#oracle)
    * [Prometheus](#prometheus)
    * [Custom](#cust)


5. Based on the database type selected, configure the database details.

 * **IBM Db2**{: #db2}

    If you select **IBM Db2** from the **Database type** drop-down list, configure the following details:

    Two databases with the same name cannot be added.
   {: note}

    | Field           | Description        |
    |------------------|--------------------|
    | Database name     | Enter the name of your database. |
    | Display name    | Enter the database name to be displayed on the screen. |
    | Hostname            | Enter the hostname.  |
    | Port             | Enter the port number. |
    | Username           | Enter the  username.  |
    | Password           | Enter the password.  |
    | Test connection     | Click the Test connection link to test the database connection. If the database connection is successful, a success message appears.|
    | Port is SSL enabled   | To establish a secure connection, do the following steps: \n i. Select the Port is SSL enabled checkbox. The Upload SSL certificate (.pem, .crt or .cer) link is enabled. \n ii. Click the Upload SSL certificate (.pem, .crt or .cer) link. \n iii. Browse the SSL certificate and upload.|
    | Catalog name | Enter the name of the catalog. This catalog is automatically associated with your database. |
    {: caption="Table 1. Register database" caption-side="bottom"}

    Select IBM Db2 from the Database Type drop-down list to add IBM Watson Query.
    You can now query the nicknames that are created in Db2 and the virtualized tables from Watson Query instances.
   {: note}

 * **IBM Netezza**{: #netezza}

    If you select **IBM Netezza** from the **Database type** drop-down list, configure the following details:

    Two databases with the same name cannot be added.
   {: note}

    | Field           | Description        |
    |------------------|--------------------|
    | Database name     | Enter the name of your database. |
    | Display name    | Enter the database name to be displayed on the screen. |
    | Hostname            | Enter the hostname.  |
    | Port             | Enter the port number. |
    | Username           | Enter the  username.  |
    | Password           | Enter the password.  |
    | Test connection     | Click the Test connection link to test the database connection. If the database connection is successful, a success message appears.|
    | Port is SSL enabled   | To establish a secure connection, do the following steps: \n i. Select the Port is SSL enabled checkbox. The Upload SSL certificate (.pem, .crt or .cer) link is enabled. \n ii. Click the Upload SSL certificate (.pem, .crt or .cer) link. \n iii. Browse the SSL certificate and upload.|
    | Catalog name | Enter the name of the catalog. This catalog is automatically associated with your database. |
    {: caption="Table 2. Register database" caption-side="bottom"}

    For a database type as Netezza, select the version 11.2.2.x.
    {: note}

 * **MongoDB**{: #mongo}

    If you select **MongoDB** from the **Database type** drop-down list, configure the following details:

    Two databases with the same name cannot be added.
   {: note}

    | Field           | Description        |
    |------------------|--------------------|
    | Database name     | Enter the name of your authentication database.|
    | Display name    | Enter the database name to be displayed on the screen. |
    | Hostname            | Enter the hostname. You can add multiple host information. To add, click the **Add** icon. A new row appears for adding hostname and port. Enter the details  |
    | Port             | Enter the port number. |
    | Username           | Enter the  username.  |
    | Password           | Enter the password.  |
    | Test connection     | Click the Test connection link to test the database connection. If the database connection is successful, a success message appears.|
    | Port is SSL enabled   | To establish a secure connection, do the following steps: \n i. Select the Port is SSL enabled checkbox. The Upload SSL certificate (.pem, .crt or .cer) link is enabled. \n ii. Click the Upload SSL certificate (.pem, .crt or .cer) link. \n iii. Browse the SSL certificate and upload.|
    | Catalog name | Enter the name of the catalog. This catalog is automatically associated with your database. |
    {: caption="Table 3. Register database" caption-side="bottom"}


 * **Apache Kafka**{: #kafka}

    If you select **Apache Kafka** from the **Database type** drop-down list, configure the following details:

    Two databases with the same name cannot be added.
   {: note}

    | Field           | Description        |
    |------------------|--------------------|
    | Display name    | Enter the database name to be displayed on the screen. |
    | Hostname            | Enter the hostname. You can add multiple host information. To add, click the **Add** icon. A new row appears for adding hostname and port. Enter the details.  |
    | Port             | Enter the port number. |
    | Username           | Enter the  username.  |
    | Password           | Enter the password.  |
    | SASL connection   | Enable the Simple Authentication Security Layer (SASL) to include authentication mechanism. If you enable SASL, specify the username and API key.|
    | Test connection     | Click the Test connection link to test the database connection. If the database connection is successful, a success message appears.|
    | Catalog name | Enter the name of the catalog. This catalog is automatically associated with your database. |
    | Add topics    | You can add topics after you create the database.  \n i. Go to the **Infrastructure manager**. \n ii. Click on the **Apache Kafka** database. \n iii. Click **Add topics** option. \n iv. Upload .json definition files. You can either drag the files or use the **Click to upload** option. Topic names are determined from the definition files. \n v. Use the **Edit** option to view and edit the topic files.|
    {: caption="Table 4. Register database" caption-side="bottom"}


 * **MySQL**{: #mysql}

    If you select **MySQL** from the **Database type** drop-down list, configure the following details:

    Two databases with the same name cannot be added.
   {: note}

    | Field           | Description        |
    |------------------|--------------------|
    | Display name    | Enter the database name to be displayed on the screen. |
    | Hostname            | Enter the hostname.  |
    | Port             | Enter the port number. |
    | Username           | Enter the  username.  |
    | Password           | Enter the password.  |
   | Test connection     | Click the Test connection link to test the database connection. If the database connection is successful, a success message appears.|
    | Port is SSL enabled   | To establish a secure connection, do the following steps: \n i. Select the Port is SSL enabled checkbox. The Upload SSL certificate (.pem, .crt or .cer) link is enabled. \n ii. Click the Upload SSL certificate (.pem, .crt or .cer) link. \n iii. Browse the SSL certificate and upload.|
    | Catalog name | Enter the name of the catalog. This catalog is automatically associated with your database. |
    {: caption="Table 5. Register database" caption-side="bottom"}


 * **Elasticsearch**{: #elastic}

    If you select **Elastcisearch** from the **Database type** drop-down list, configure the following details:

    Two databases with the same name cannot be added.
   {: note}

    | Field           | Description        |
    |------------------|--------------------|
    | Display name    | Enter the database name to be displayed on the screen. |
    | Hostname            | Enter the hostname.  |
    | Port             | Enter the port number. |
    | Username           | Enter the  username.  |
    | Password           | Enter the password.  |
    | SSL Connection   | To establish a secure connection, do the following steps: \n i. Select the SSL Connection checkbox. The Upload SSL certificate (.pem, .crt or .cer) link is enabled. \n ii. Click the Upload SSL certificate (.pem, .crt or .cer) link. \n iii. Browse the SSL certificate and upload.|
    | Catalog name | Enter the name of the catalog. This catalog is automatically associated with your database. |
    {: caption="Table 6. Register database" caption-side="bottom"}


 * **SQL Server**{: #sql}

    If you select **SQL Server** from the **Database type** drop-down list, configure the following details:

    Two databases with the same name cannot be added.
   {: note}

    | Field           | Description        |
    |------------------|--------------------|
    | Database name     | Enter the name of your database.|
    | Display name    | Enter the database name to be displayed on the screen. |
    | Hostname            | Enter the hostname.  |
    | Port             | Enter the port number. |
    | Username           | Enter the  username.  |
    | Password           | Enter the password.  |
    | Test connection     | Click the Test connection link to test the database connection. If the database connection is successful, a success message appears.|
    | Port is SSL enabled   | To establish a secure connection, do the following steps: \n i. Select the Port is SSL enabled checkbox. The Upload SSL certificate (.pem, .crt or .cer) link is enabled. \n ii. Click the Upload SSL certificate (.pem, .crt or .cer) link. \n iii. Browse the SSL certificate and upload.|
    | Catalog name | Enter the name of the catalog. This catalog is automatically associated with your database. |
    {: caption="Table 7. Register database" caption-side="bottom"}


 * **PostgreSQL**{: #postgresql}

    If you select **PostgreSQL** from the **Database type** drop-down list, configure the following details:

    Two databases with the same name cannot be added.
   {: note}

    | Field           | Description        |
    |------------------|--------------------|
    | Database name     | Enter the name of your database.|
    | Display name    | Enter the database name to be displayed on the screen. |
    | Hostname            | Enter the hostname.  |
    | Port             | Enter the port number. |
    | Username           | Enter the  username.  |
    | Password           | Enter the password.  |
    | Test connection     | Click the Test connection link to test the database connection. If the database connection is successful, a success message appears.|
    | Port is SSL enabled   | To establish a secure connection, do the following steps: \n i. Select the Port is SSL enabled checkbox. The Upload SSL certificate (.pem, .crt or .cer) link is enabled. \n ii. Click the Upload SSL certificate (.pem, .crt or .cer) link. \n iii. Browse the SSL certificate and upload.|
    | Validate Certificate           | Enable it to validate whether the SSL certificate that is returned by the host is trusted or not.  |
    | Catalog name | Enter the name of the catalog. This catalog is automatically associated with your database. |
    {: caption="Table 8. Register database" caption-side="bottom"}


 * **SingleStore**{: #singlestore}

    If you select **SingleStore** from the **Database type** drop-down list, configure the following details:

    Two databases with the same name cannot be added.
   {: note}

    | Field           | Description        |
    |------------------|--------------------|
    | Database name     | Enter the name of your database.|
    | Display name    | Enter the database name to be displayed on the screen. |
    | Hostname            | Enter the hostname.  |
    | Port             | Enter the port number. |
    | Username           | Enter the  username.  |
    | Password           | Enter the password.  |
    | Test connection     | Click the Test connection link to test the database connection. If the database connection is successful, a success message appears.|
    | Port is SSL enabled     | To establish a secure connection, do the following steps: \n i. Select the Port is SSL enabled checkbox. The Upload SSL certificate (.pem, .crt or .cer) link is enabled. \n ii. Click the Upload SSL certificate (.pem, .crt or .cer) link. \n iii. Browse the SSL certificate and upload.|
    | Catalog name | Enter the name of the catalog. This catalog is automatically associated with your database. |
    {: caption="Table 9. Register database" caption-side="bottom"}


 * **Teradata**{: #teradata}

    If you select **Teradata** from the **Database type** drop-down list, configure the following details:

    Two databases with the same name cannot be added.
   {: note}

    | Field           | Description        |
    |------------------|--------------------|
    | Database name     | Enter the name of your database.|
    | Display name    | Enter the database name to be displayed on the screen. |
    | Hostname            | Enter the hostname.  |
    | Port             | Enter the port number. |
    | Username           | Enter the  username.  |
    | Password           | Enter the password.  |
    |SSL Connection     | To establish a secure connection, do the following steps: \n i. Select the SSL Connection checkbox. The Upload SSL certificate (.pem, .crt or .cer) link is enabled. \n ii. Click the Upload SSL certificate (.pem, .crt or .cer) link. \n iii. Browse the SSL certificate and upload.|
    | Catalog name | Enter the name of the catalog. This catalog is automatically associated with your database. |
    {: caption="Table 10. Register database" caption-side="bottom"}

 * **Snowflake**{: #snowflake}

    If you select **Snowflake** from the **Database type** drop-down list, configure the following details:

    Two databases with the same name cannot be added.
   {: note}

    | Field           | Description        |
    |------------------|--------------------|
    | Database name     | Enter the name of your database.|
    | Display name    | Enter the database name to be displayed on the screen. |
    | Hostname            | Enter the hostname.  |
    | Username           | Enter the  username.  |
    | Password           | Enter the password.  |
    | Catalog name | Enter the name of the catalog. This catalog is automatically associated with your database. |
    {: caption="Table 11. Register database" caption-side="bottom"}

 * **IBM Data Virtualization Manager for z/OS**{: #dvm}

    If you select **IBM Data Virtualization Manager for z/OS** from the **Database type** drop-down list, configure the following details:

    Two databases with the same name cannot be added.
   {: note}

    | Field           | Description        |
    |------------------|--------------------|
    | Display name    | Enter the database name to be displayed on the screen. |
    | Hostname            | Enter the hostname.  |
    | Port             | Enter the port number. |
    | Username           | Enter the  username.  |
    | Password           | Enter the password.  |
    | Port is SSL enabled   | To establish a secure connection, do the following steps: \n i. Select the Port is SSL enabled checkbox. The Upload SSL certificate (.pem, .crt or .cer) link is enabled. \n ii. Click the Upload SSL certificate (.pem, .crt or .cer) link. \n iii. Browse the SSL certificate and upload.|
    | Validate Certificate           | Enable it to validate whether the SSL certificate that is returned by the host is trusted or not.  |
    | Hostname in SSL certificate           | Provide the hostname in SSL certificate. This step is optional.  |
    | Catalog name | Enter the name of the catalog. This catalog is automatically associated with your database. |
    {: caption="Table 12. Register database" caption-side="bottom"}


 * **Amazon Redshift**{: #amazon}

    If you select **Amazon Redshift** from the **Database type** drop-down list, configure the following details:

    Two databases with the same name cannot be added.
   {: note}

    | Field           | Description        |
    |------------------|--------------------|
    | Database name     | Enter the name of your database. |
    | Display name    | Enter the database name to be displayed on the screen. |
    | Hostname            | Enter the hostname.  |
    | Port             | Enter the port number. |
    | Username           | Enter the  username.  |
    | Password           | Enter the password.  |
    | SSL connection   | To establish a secure connection, do the following steps: \n i. Select the SSL connection checkbox. The Upload SSL certificate (.pem, .crt or .cer) link is enabled. \n ii. Click the Upload SSL certificate (.pem, .crt or .cer) link. \n iii. Browse the SSL certificate and upload.|
    | Validate Certificate   | Enable it to validate whether the SSL certificate that is returned by the host is trusted or not. |
    | Catalog name | Enter the name of the catalog. This catalog is automatically associated with your database. |
    {: caption="Table 13. Register database" caption-side="bottom"}


 * **Informix**{: #informix}

    If you select **Informix** from the **Database type** drop-down list, configure the following details:

    Two databases with the same name cannot be added.
   {: note}

    | Field           | Description        |
    |------------------|--------------------|
    | Database name     | Enter the name of your database. |
    | Display name    | Enter the database name to be displayed on the screen. |
    | Hostname            | Enter the hostname.  |
    | Port             | Enter the port number. |
    | Username           | Enter the  username.  |
    | Password           | Enter the password.  |
    | Informix server     | Enter the Informix server name.|
    | SSL connection   | To establish a secure connection, do the following steps: \n i. Select the SSL connection checkbox. The Upload SSL certificate (.pem, .crt or .cer) link is enabled. \n ii. Click the Upload SSL certificate (.pem, .crt or .cer) link. \n iii. Browse the SSL certificate and upload.|
    | Catalog name | Enter the name of the catalog. This catalog is automatically associated with your database. |
    {: caption="Table 14. Register database" caption-side="bottom"}


 * **Oracle**{: #oracle}

    If you select **Oracle** from the **Database type** drop-down list, configure the following details:

    Two databases with the same name cannot be added.
   {: note}

    | Field           | Description        |
    |------------------|--------------------|
    | Database name     | Enter the name of your database. |
    | Display name    | Enter the database name to be displayed on the screen. |
    | Hostname            | Enter the hostname.  |
    | Port             | Enter the port number. |
    | Username           | Enter the  username.  |
    | Password           | Enter the password.  |
    | Connection mode     | Enter the connection mode.|
    | Connection mode value     | Enter the connection mode value.|
    | Port is SSL enabled   | To establish a secure connection, do the following steps: \n i. Select the Port is SSL enabled checkbox. The Upload SSL certificate (.pem, .crt or .cer) link is enabled. \n ii. Click the Upload SSL certificate (.pem, .crt or .cer) link. \n iii. Browse the SSL certificate and upload.|
    | Catalog name | Enter the name of the catalog. This catalog is automatically associated with your database. |
    {: caption="Table 15. Register database" caption-side="bottom"}


 * **Prometheus**{: #prometheus}

    If you select **Prometheus** from the **Database type** drop-down list, configure the following details:

    Two databases with the same name cannot be added.
   {: note}

    | Field           | Description        |
    |------------------|--------------------|
    | Database name     | Enter the name of your database. |
    | Display name    | Enter the database name to be displayed on the screen. |
    | Hostname            | Enter the hostname.  |
    | Port             | Enter the port number. |
    | Port is SSL enabled   | To establish a secure connection, do the following steps: \n i. Select the Port is SSL enabled checkbox. The Upload SSL certificate (.pem, .crt or .cer) link is enabled. \n ii. Click the Upload SSL certificate (.pem, .crt or .cer) link. \n iii. Browse the SSL certificate and upload.|
    | Verify hostname | Enable it to verify hostname in the SSL certificate. |
    | Catalog name | Enter the name of the catalog. This catalog is automatically associated with your database. |
    {: caption="Table 16. Register database" caption-side="bottom"}


 * **Custom**{: #cust}

    If you select **Custom** from the **Database type** drop-down list, configure the following details:

    Two databases with the same name cannot be added.
   {: note}

    Custom databases do not support SSL configuration properties.
   {: note}

   Custom database feature can be used for connectors that are already supported by Presto but not listed in IBM {{site.data.keyword.lakehouse_full}} supported connectors or databases.

   For more information, see [Custom database feature](watsonxdata?topic=watsonxdata-custom_database).

6. Click **Add**.
