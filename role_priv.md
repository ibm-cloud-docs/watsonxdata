---

copyright:
  years: 2022, 2023
lastupdated: "2023-11-29"

keywords: lakehouse, watsonx data, privileges, roles, access

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

# Managing roles and privileges
{: #role_priv}

A role is a set of privileges that is assigned to a user to allow the user to perform and manage certain tasks in {{site.data.keyword.lakehouse_full}}.
{: shortdesc}

{{site.data.keyword.lakehouse_short}} provides a set of predefined roles: Administrator, User, Manager, Writer, and Reader.

Use the **Access control** page to manage users and roles in {{site.data.keyword.lakehouse_short}}. For more information, see [Managing user access](watsonxdata?topic=watsonxdata-manage_access).

The following tables describe the privileges that you can assign to roles and associated permissions:

## Engine (Presto)
{: #engine_role}

| Privileges | Administrator | Manager | User without a role |
|--------------------------|----------------|--------|--------|
| Delete an engine | Y | N | N |
| Grant access  | Y | N | N |
| Revoke access | Y | N | N |
| Pause an engine | Y | Y | N |
| Resume an engine | Y | Y | N |
| Restart an engine | Y | Y | N |
| Associate a catalog | Y | Y | N |
| Disassociate a catalog | Y | Y | N |
| Access the Presto query monitor UI | Y | Y | N |
| View existence  | Y | Y | N |
{: caption="Table 1. Roles and privileges for an engine" caption-side="bottom"}

## Catalog
{: #catalog_role}

| Privileges | Administrator | User | User without a role |
|--------------------------|----------------|--------|--------|
| Delete a catalog | Y | N | N |
| Grant access | Y | N | N |
| Revoke access | Y | N | N |
| Create any schema | Y | N | N |
| Drop any schema | Y | N | N |
| Select from data | Y | Y | N |
| Drop own schema | Y | N | N |
| View existance | Y | Y | Y |
{: caption="Table 2. Roles and privileges for a catalog" caption-side="bottom"}

## Bucket
{: #bucket_role}

| Privileges | Administrator | Writer | Reader | User without a role |
|--------------------------|----------------|--------|--------|--------|
| Unregister | Y | N | N | N |
| Update bucket properties (credentials) | Y | N | N | N |
| Grant access | Y | N | N | N |
| Revoke access | Y | N | N | N |
| Create catalog | Y | N | N | N |
| Modify files into the bucket | Y | Y | N | N |
| Browse (bucket browser in UI) | Y | Y | Y | N |
| View existance | Y | Y | Y | Y |
{: caption="Table 3. Roles and privileges for a bucket" caption-side="bottom"}

## Database
{: #database_role}

| Privileges | Administrator | Writer | Reader | User without a role |
|--------------------------|----------------|--------|--------|--------|
| Unregister | Y | N | N | N |
| Update database connection properties (credentials) | Y | N | N | N |
| Grant access| Y | N | N | N |
| Revoke access | Y | N | N | N |
| Create catalog | Y | N | N | N |
| Modify database objects | Y | Y | N | N |
| Browse remote data (when connected to an engine) | Y | Y | Y | N |
| View existance | Y | Y | Y | Y | Y |
{: caption="Table 4. Roles and privileges for a database" caption-side="bottom"}

## Schema
{: #schema_role}

| Privileges |Catalog Administrator or Schema creator | Others |
|--------------------------|----------------|--------|
| Grant access| Y | N |
| Revoke access | Y | N |
| Column access | Y | N |
| Create table | Y | N |
{: caption="Table 4. Roles and privileges for a schema" caption-side="bottom"}

## Table
{: #table_role}

| Privileges |Catalog Administrator or Schema Administrator or Table creator | Others |
|--------------------------|----------------|--------|
| Create | Y | N |
| Drop | Y | N |
| Alter | Y | N |
| Column access | Y | N |
| Select | Y | N |
| Insert | Y | N |
| Update | Y | N |
| Delete | Y | N |
{: caption="Table 4. Roles and privileges for a table" caption-side="bottom"}

Where

Y indicates that members of this role have this permission.
N indicates that members of this role do not have this permission.
