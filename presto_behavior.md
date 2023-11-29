---

copyright:
  years: 2022, 2023
lastupdated: "2023-11-29"

keywords: lakehouse, netezza, connector, watsonx.data

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

# Presto case-sensitive behavior
{: #presto_behavior}

The Presto behavior is changed from case-insensitive to case-sensitive. User needs to provide the query name in original case format as in database.
{: shortdesc}

## Code changes
{: #code_changes}

The following database objects are case-sensitive:
* Schema Names
* Table Names
* Column Names

Catalog names are still converted to lowercase letters.
{: note}

## Case-sensitive behavior for JDBC connectors
{: #case-sensitive_behavior}

JDBC connectors had an extra conversion to uppercase based on the flag setting in the corresponding driver jar - the method, storesUpperCaseIdentifiers(), from DatabaseMetadata object of the JDBC driver. If the method returns true for a particular connector, for example, Db2, the object name that the user entered gets converted to uppercase before it is moved to the database. To override this behavior, a new connector level parameter is introduced. The new parameter checkDriverCaseSupport is by default false, which means presto doesn't consider driver-specific case, but if configured as true, it can go back to the old behavior for that connector.

Users can add the parameter check-driver-case-support in their catalog.porperties file to use the connector's default case format. For example, Db2 and {{site.data.keyword.netezza_full}} store identifiers in uppercase by default unless user wraps the identifier name within double quotation marks. For example, the following query creates a table as EMPLOYEE if it is run in Db2:

   `create table employee(id int, name varchar(10));`

In presto, double quotation marks are intentionally added around schema names and table names to enable mixed case support.

If a user wants to create objects in Db2 or {{site.data.keyword.netezza_full}} through presto in uppercase, they can add the following property in the catalog.properties file:

   `check-driver-case-support = true`

This feature is only applicable to JDBC connectors.
{: note}

## Changes in User Experience
{: #changes_ux}

The following features are available for UI:

* The objects are visible as they are stored in the database.
* Users can create Schemas, Tables and Columns in mixed case that is, uppercase and lowercase through Presto if the database supports it.
* Users must write case-sensitive queries. For example, all the following query combinations that used to work for a Db2 connector earlier, even though the TABLE NAME was stored as DEPARTMENTS in the database:
1. SELECT * FROM "db2"."AMPERS"."DEPARTMENTS";
2. SELECT * FROM "db2".AMPERS.DEPARTMENTS;
3. SELECT * FROM "db2"."ampers"."departments";
4. SELECT * FROM "db2".ampers.departments;

Now, as Presto is case-sensitive, only the following queries are valid:
1. SELECT * FROM "db2"."AMPERS"."DEPARTMENTS";
2. SELECT * FROM "db2".AMPERS.DEPARTMENTS;

The following queries result in the error "Table 'db2.ampers.departments' does not exist."
1. SELECT * FROM "db2"."ampers"."departments";
2. SELECT * FROM "db2".ampers.departments;

## Impact on connectors
{: #Impact_connectors}

Since the HMS stores objects in lowercase, no change is observed in the behavior, though Presto behavior is changed.

For Hive and Iceberg connectors, the following query combinations are valid:
1. SELECT * FROM "iceberg_data"."testsch"."employee";
2. SELECT * FROM "iceberg_data".testsch.employee;
3. SELECT * FROM "iceberg_data"."TESTSCH"."employee";
4. SELECT * FROM "iceberg_data".TESTSCH"."EMPLOYEE";

Currently, the case restriction applies when tables are created in Hive and Iceberg. The user needs to specify the schema name in lowercase itself as it is stored internally in lowercase, even though the Select and Insert queries work case - insensitively.
{: note}
