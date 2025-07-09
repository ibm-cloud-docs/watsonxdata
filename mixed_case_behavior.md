---

copyright:
  years: 2022, 2025
lastupdated: "2025-07-01"

keywords: lakehouse, mixed-case behavior, watsonx.data

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

# Mixed-case behavior
{: #mixed_case_behavior}

From IBM® watsonx.data version 2.0.0, a new feature is available to switch between both case-sensitive and case-insensitive behavior in Presto (Java) by using a mixed-case feature flag. The mixed-case feature flag is set to OFF in Presto (Java) by default. The flag can be set to ON or OFF as required during deployment of the Presto (Java) engine. It is advised not to toggle between ON and OFF configurations after the deployment, as it may result in inconsistent system behavior. This feature is not applicable for Presto (C++) engine.
{: shortdesc}

## Mixed-case feature flag: ON
{: #flagon_features}

The following section lists the behaviors of connectors if mixed-case feature flag is set to ON:

   * **General behavior for all connectors**:

     * Column names in the `SELECT` query are case-insensitive.

     * While referencing the data within the `WITH` clause, it is essential to use the exact alias name (case-sensitive) assigned during its definition. Using an incorrect alias triggers the following error message: "Schema must be specified when session schema is not set."


     * For tables that are specified using `WITH` and `USE` catalog.schema clauses, the alias name is case-sensitive. Using an incorrect alias triggers the following error message: "Table does not exist."

   * **Hive**:

     * The alias name is case-sensitive for `WITH` clause.
     * When using column names in the `INSERT` query, use only lowercase.

   * **Iceberg**:

     * The alias name is case-sensitive for `WITH` clause.
     * When using column names in the `INSERT` query, use only lowercase.

   * **MongoDB**:

     * Column names for `DELETE` statement are case-insensitive.

   * **Teradata**:

     * Tables with duplicate names cannot be created, regardless of the case.

   * **IBM **{{site.data.keyword.netezza_short}}****:

     * Tables with the same name and case cannot exist in multiple schemas that have the same name but different cases.

   * **Delta Lake**:

     * Schema name in `SELECT` statement is case-sensitive.

   * **Amazon Redshift**:

      * In the Amazon Redshift server, all the identifiers are case-sensitive if the configuration is set as:

      ```bash
         enable_case_sensitive_identifier=true
      ```
      {: codeblock}


      * In the Amazon Redshift server, only lowercase identifiers are fetched if the configuration is set as:

      ```bash
         enable_case_sensitive_identifier=false
      ```
      {: codeblock}

   * **SQL Server**:

     * Enable case-sensitive collation in the SQL Server to create duplicate tables in mixed-case.

   * **Apache Pinot**:

     * Schema name is case insensitive irrespective of the case sensitivity of Presto (Java) engine behavior.

## Mixed-case feature flag: OFF
{: #flagoff_features}

The following section lists the behaviors of connectors if mixed-case feature flag is set to OFF:

   * **MariaDB**:

     * Table and schema names should be in lowercase.

   * **Greenplum**:

     * Table and schema names should be in lowercase.

   * **IBM {{site.data.keyword.netezza_short}}**:

     * Schema name for `USE` statement is case-sensitive if you use it before `CREATE VIEW` statement.

   * **Db2**:

     * Schema name for `USE` statement is case-sensitive if you use it before `CREATE VIEW` statement.

For more information on mixed-case feature flag behavior, supported SQL statements and supported data types matrices, see [Support content](https://www.ibm.com/support/pages/node/7157339){: external}.
{: important}
