---

copyright:
  years: 2022, 2024
lastupdated: "2024-04-30"

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

Access control policies might also be affected after an upgrade.
{: note}

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

In the open source Presto, the JDBC databases that internally store objects in uppercase, for example, Db2 and Netezza® Performance Server, the object names that the user entered used to get converted to uppercase. As Presto now supports mixed case, this behavior is slightly changed. A new connector level parameter check-driver-case-support is introduced. This parameter is by default false, indicating that Presto doesn't consider database-specific case. This parameter is expected to be available in the UI in the future releases so that it can be set as true or false.

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

## Impact on Iceberg and Hive catalogs
{: #Impact_connectors}

Since the HMS stores objects in lowercase, no change is observed in the behavior, though Presto behavior is changed.

For Hive and Iceberg catalogs, the following query combinations are valid:
1. SELECT * FROM "iceberg_data"."testsch"."employee";
2. SELECT * FROM "iceberg_data".testsch.employee;
3. SELECT * FROM "iceberg_data"."TESTSCH"."employee";
4. SELECT * FROM "iceberg_data".TESTSCH"."EMPLOYEE";

Currently, the case restriction applies when tables are created in Hive and Iceberg. The user needs to specify the schema name in lowercase itself as it is stored internally in lowercase, even though the Select and Insert queries work case - insensitively.
{: note}
