---

copyright:
  years: 2022, 2024
lastupdated: "2024-11-30"

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

 Configure the following details for MySQL data source:

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
 | Catalog name | Enter the name of the catalog. This catalog is automatically associated with your data source. |
 | Create | Click Create to create the data source. |
 {: caption="Register data source" caption-side="bottom"}

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
