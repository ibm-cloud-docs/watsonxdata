---

copyright:
  years: 2022, 2025
lastupdated: "2025-08-01"

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

For more information on mixed-case feature flag behavior, supported SQL statements and supported data types matrices, see [Support content](https://www.ibm.com/support/pages/node/7157339){: external}.
{: important}

## Mixed-case feature flag: ON
{: #flagon_features}

You can enable mixed-case identifiers (schema, table, and column names) per catalog using a global API configuration in Presto (Java). When you set the global property `enable-mixed-case-support=true`, the system automatically enables a catalog-level property `case-sensitive-name-matching=true` for all eligible catalogs.

The following catalogs support the `case-sensitive-name-matching` property:

- HANA
- MySQL
- Oracle
- PostgreSQL
- Amazon Redshift
- SingleStore
- SQL Server
- IBM Db2
- IBM Data Virtualization Manager
- IBM Db2fori
- IBM Informix
- IBM Netezza
- Apache Phoenix
- Snowflake
- Teradata
- Greenplum
- Apache Derby
- MariaDB

Presto defaults the `case-sensitive-name-matching` configuration to `false` for all eligible catalogs.
{: note}

## Mixed-case feature flag: OFF
{: #flagoff_features}

When `case-sensitive-name-matching=false` (the default setting), Presto (Java) converts identifiers to lowercase. This is the default behavior in Presto.
