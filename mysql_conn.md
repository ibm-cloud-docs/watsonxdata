---

copyright:
  years: 2022, 2025
lastupdated: "2025-08-25"

keywords: lakehouse, data source, watsonx.data

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

# MySQL
{: #mysql_database}

MySQL is an open source relational database management system.
{: shortdesc}

You can configure MySQL using one of the following methods:
- `Create new connection` – If you select the `Create new connection` tab, refer to the [Create new connection - configuration details](/docs/watsonxdata?topic=watsonxdata-mysql_database#mysql_database1) table to provide configuration details.

- `Import from catalog` – You can import connection details from an existing catalog in the data platform. If you select the `Import from catalog` tab, refer to the [Import from catalog - configuration details](/docs/watsonxdata?topic=watsonxdata-mysql_database#mysql_database2) table to provide configuration details.

- `Import from project` – You can import connection details from an existing project in the data platform. If you select `Import from project`, refer to the [Import from project - configuration details](/docs/watsonxdata?topic=watsonxdata-mysql_database#mysql_database3) table to provide configuration details.

## Create new connection - configuration details
{: #mysql_database1}

 | Field           | Description        |
 |------------------|--------------------|
 | Display name    | Enter the data source name to be displayed on the screen. |
 | Database name     | Enter the name of your database. |
 | Hostname            | Enter the hostname.  |
 | Port             | Enter the port number. |
 | Username           | Enter the username.  |
 | Password           | Enter the password.  |
 | Port is SSL enabled   | Use the toggle switch to enable or disable SSL connection. If enabled, \n i. The Upload SSL certificate (.pem, .crt, .cert or .cer) link is enabled. \n ii. Click the Upload SSL certificate (.pem, .crt, .cert or .cer) link. \n iii. Browse the SSL certificate and upload.|
 | Validate certificate           | Use the toggle switch to validate whether the SSL certificate that is returned by the host is trusted or not.  |
 | Connection status| Click the Test connection link to test the data source connection. If the data source connection is successful, a success message appears. You must add a JAR as part of the Bring Your Own JAR (BYOJ) process to enable the test connection option.|
 | Associated catalog| Select the checkbox to associate a catalog to the data source. This catalog is automatically associated with your data source and serves as your query interface with the data stored within.|
 | Catalog name | Enter the name of the catalog.|
 | Create | Click Create to create the data source. |
 {: caption="Crete new connection - configuration details" caption-side="bottom"}

## Import from catalog - configuration details
{: #mysql_database2}

 | Field | Description |
| --- | --- |
| Select catalog | Use the dropdown to select a catalog. |
| Select data source | Use the dropdown to select a data source from the selected catalog. |
| Connection status | Click the Test connection link to test the database connection. If the database connection is successful, a success message appears. |
| Display name | Enter the database name to be displayed on the screen. |
| Associate catalog | Select the checkbox to associate a catalog to the data source. This catalog is automatically associated with your data source and serves as your query interface with the data stored within. |
| Catalog name | Enter the name of the catalog. |
| Create | Click Create to create the database. |
{: caption="Import from catalog - configuration details" caption-side="bottom"}


## Import from project - configuration details
{: #mysql_database3}

| Field | Description |
| --- | --- |
| Select project | Use the dropdown to select a project. |
| Select data source | Use the dropdown to select a data source from the selected project |
| Connection status | Click the Test connection link to test the database connection. If the database connection is successful, a success message appears. |
| Display name | Enter the database name to be displayed on the screen. |
| Associate catalog | Select the checkbox to associate a catalog to the data source. This catalog is automatically associated with your data source and serves as your query interface with the data stored within. |
| Catalog name | Enter the name of the catalog. |
| Create | Click Create to create the database. |
{: caption="Import from project - configuration details" caption-side="bottom"}

## Bring Your Own JAR (BYOJ) Process
 {: #mysql_byoj}

The following is the procedure to add your own JAR to the MySQL data source:
1. Log in to the IBM® watsonx.data instance.
2. From the navigation menu, go to the Configurations page and click the Driver manager tile.
3. Click Add driver.
4. Upload the MySQL JAR and specify the driver version. Currently, only one JAR(mysql-connector-j-8.2.0.jar) is supported for MySQL dadata source.
5. Click Add. Once the driver is successfully added, it undergoes a series of validation. If the validation is successful, it is set to 'inactive' status otherwise it is set to 'failed' status.
6. Click the vertical ellipsis icon to assign or delete the driver.
7. To assign the driver to an engine:
   * Click Assign.
   * Select one or more engines to assign the driver. Once assigned, the driver is set to 'active' status.
8. To unassign a driver from an engine, users must first introduce another driver.
9. Click Save and restart engine.
10. In the Infrastructure manager, hover over the MySQL data source and click the Manage associations icon.
11. Select the engine to modify the catalog's association with it. All in-flight queries on the modified engines are stopped.
12. Click Save and restart engine.

You can link the MySQL data source to the engine only when a driver is associated to that engine. Only one MySQL driver can be associated to an engine at a time.
{: note}

## Vulnerabilities in JAR
{: #mysql_vul}

As part of the BYOJ process, users can upload the required JAR files. If a vulnerability is identified in a JAR, a grace period is set for the removal and cleanup activities based on the severity of the security vulnerability as shown in the following table:

| Severity of vulnerability | Grace period (in days) |
 |--------------------------|----------------|
 | Critical | 30|
 | High     | 60 |
 | Medium   | 120 |
 | Low      | 180 |
 {: caption="Vulnerability and grace period" caption-side="bottom"}

The grace period is calculated from the date the vulnerability is reported, plus the specified grace period. Multiple warnings are displayed to the users about the grace period in the Driver manager page (for the admin) as well as in other places like in the ‘Catalogs’ section in the ‘Infrastructure manager’ page and in the ‘Catalogs associated’ section in the ‘Data manager page’. For example, if a customer uses the mysql-connector-j-8.2.0.jar and a critical vulnerability is identified on October 1st, a cleanup process begins immediately after October 31st. This process deletes the driver from the bucket and Presto pods, disassociates the catalog from the engine, disassociates the driver in the Driver Manager page, and deletes the entry.

## Upgrade impact on MySQL catalogs (version 2.1.0)
{: #mysql_upgrade}

**What to expect after the upgrade to watsonx.data version 2.1.0:**

When you upgrade to watsonx.data version 2.1.0, existing MySQL catalogs are disassociated with the engine. This means, you must reassociate the MySQL catalog with the engine.

**Steps to reassociate MySQL catalog:**

To reassociate the MySQL catalog with the engine, upload the mysql-connector-j:8.2.0 JAR file to the driver manager by following the BYOJ process.

## Limitations for SQL statements
{: #connector_limitations}

* Only `CREATE TABLE AS` is supported for `CREATE TABLE` statement.
* `DROP TABLE` statement is supported only when enabled in the catalog.
* For data source-based catalogs the `CREATE SCHEMA`, `CREATE TABLE`, `DROP SCHEMA`, `DROP TABLE`, `DELETE`, `DROP VIEW`, `ALTER TABLE`, and `ALTER SCHEMA` statements are not available in the **Data Manager** UI.

## Limitations for data types
{: #connector_limitations2}

* `BLOB` and `CLOB` data types support `SELECT` statement but do not support operations such as `equal`, `like`, and `in`.
* `BINARY` data type supports only `SELECT` statement.
* The data that is shown from the UI for `BLOB` data type is in Base64 format, while the result from presto-cli is in hexadecimal format.
* The data that is shown from the UI for `BINARY` data type is in Base64 format, while the result from presto-cli is in hexadecimal format.
* You can use `CLOB` data type as an equivalent alternative to `LONGTEXT`.
* When the fields of data type `REAL` have 6 digits or more in the decimal part with the digits being predominately zero, the values when queried are rounded off. It is observed that the rounding off occurs differently based on the precision of the values. For example, a decimal number 1.654 when rounded to 3-digits after the decimal point are the same. Another example is 10.890009 and 10.89000. It is noticed that 10.89000 is rounded to 10.89, whereas 10.89009 is not rounded off. This is an inherent issue because of the representational limitations of binary floating point formats. This might have a significant impact when querying involves sorting.
