---

copyright:
  years: 2022, 2024
lastupdated: "2024-08-01"

keywords: lakehouse, storage, catalog, watsonx.data

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

# SAP HANA
{: #saphana_conn}

SAP HANA is a column-oriented, in-memory relational database.
{: shortdesc}

Configure the following details for SAP HANA data source:

 | Field | Description |
 |--------------------------|----------------|
 | Display name | Enter the name to be displayed.|
 | Database name | Enter the name of your database.|
 | Hostname            | Enter the hostname.  |
 | Port             | Enter the port number. |
 | Username           | Enter the username.  |
 | Password           | Enter the password.  |
 | SSL connection   | Use the toggle switch to enable or disable SSL connection. If enabled, \n i. The Upload SSL certificate (.pem, .crt, .cert or .cer) link is enabled. \n ii. Click the Upload SSL certificate (.pem, .crt, .cert or .cer) link. \n iii. Browse the SSL certificate and upload.|
 | Validate certificate     | Use the toggle switch to validate whether the SSL certificate that the host returns is trusted or not.|
 | Catalog name | Enter the name of the catalog. This catalog is automatically associated with your database. |
 | Create | Click Create to create the database. |
 {: caption="Register database" caption-side="bottom"}

## Bring Your Own JAR (BYOJ) Process
 {: #saphana_byoj}

The following is the procedure to add your own JAR to the SAP HANA database:
1. Log in to the IBM® watsonx.data console.
2. From the navigation menu, go to the Configurations page and click the Driver manager tile.
3. Click Add driver.
4. Upload the SAP HANA JAR and specify the driver version. Currently, only one JAR(ngdbc-2.17.12.jar) is supported for SAP HANA database.
5. Click Add. Once the driver is successfully added, it undergoes a series of validation. If the validation is successful, it is set to 'inactive' status otherwise it is set to 'failed' status.
6. Click the vertical ellipsis icon to assign or delete the driver.
7. To assign the driver to an engine:
   * Click Assign.
   * Select one or more engines to assign the driver. Once assigned, the driver is set to 'active' status.

Note: You can link the SAP HANA database to the engine only when a driver is associated to that engine. Only one SAP HANA driver can be associated to an engine at a time.
{: note}

8. To unassign a driver from an engine, users must first introduce another driver.
9. Click Save and restart engine.
10. In the Infrastructure manager, hover over the SAP HANA database and click the Manage associations icon.
11. Select the engine to modify the catalog's association with it. All in-flight queries on the modified engines are stopped.
12. Click Save and restart engine.

## Vulnerabilities in JAR
{: #saphana_vul}

As part of the BYOJ process, users can upload the required JAR files. If a vulnerability is identified in a JAR, a grace period is set for the removal and cleanup activities based on the severity of the security vulnerability as shown in the following table:

| Severity of vulnerability | Grace period (in days) |
 |--------------------------|----------------|
 | Critical | 30|
 | High     | 60 |
 | Medium   | 120 |
 | Low      | 180 |
 {: caption="Vulnerability and grace period" caption-side="bottom"}

The grace period is calculated from the date the vulnerability is reported, plus the specified grace period. Multiple warnings are displayed to the users about the grace period in the Driver manager page (for the admin) as well as in other places like in the ‘Catalogs’ section in the ‘Infrastructure manager’ page and in the ‘Catalogs associated’ section in the ‘Data manager page’. For example, if a customer uses the ngdbc-2.17.12.jar and a critical vulnerability is identified on October 1st, a cleanup process begins immediately after October 31st. This process deletes the driver from the bucket and Presto pods, disassociates the catalog from the engine, disassociates the driver in the Driver Manager page, and deletes the entry.

## Limitations for SQL statements
{: #connector_limitations}

* `DROP TABLE` statement is supported only when enabled in the catalog.
* By default, SAP HANA creates `VARCHAR` columns with a size of 1. So, if a base table column is defined with just `VARCHAR` without specifying a size (For example, VARCHAR(size)), then `CTAS` (Create Table As Select) operations do not work.
* For data source-based catalogs the `CREATE SCHEMA`, `CREATE TABLE`, `DROP SCHEMA`, `DROP TABLE`, `DELETE`, `DROP VIEW`, `ALTER TABLE`, and `ALTER SCHEMA` statements are not available in the **Data Manager** UI.

## Limitations for data types
{: #connector_limitations2}

* `BLOB` and `CLOB` data types support only `CREATE` and `SELECT` statements.
* `BINARY` data type supports only `SELECT` statement.
* The data that is shown for the `BLOB` and `BINARY` data types from the UI is in Base64 format, while the result from presto-cli is in hexadecimal format.
* When the fields of data type `REAL` have 6 digits or more in the decimal part with the digits being predominately zero, the values when queried are rounded off. It is observed that the rounding off occurs differently based on the precision of the values. For example, a decimal number 1.654 when rounded to 3-digits after the decimal point are the same. Another example is 10.890009 and 10.89000. It is noticed that 10.89000 is rounded to 10.89, whereas 10.89009 is not rounded off. This is an inherent issue because of the representational limitations of binary floating point formats. This might have a significant impact when querying involves sorting.
