---

copyright:
  years: 2022, 2026
lastupdated: "2026-03-10"

keywords: watsonxdata, scope, resource

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

# Account‑scoped metadata model
{: #account_scope}

The account‑scoped metadata model centralizes the management of metadata objects across all {{site.data.keyword.lakehouse_full}} instances that belong to the same IBM Cloud account and region. Instead of isolating metadata within a single instance, the platform now stores catalogs, schemas, tables, data sources, and object storages at the account level. This model enables consistent governance, easier reuse, and unified visibility across instances.
{: shortdesc}

In {{site.data.keyword.lakehouse_short}} 2.3.1 release, the **Account‑scoped** mode is available for the {{site.data.keyword.lakehouse_short}} Enterprise edition in Tokyo and Sydney SaaS regions only.
{: note}

# Overview of the account‑scoped model
{: #account_scope_1}

In earlier versions, each instance used its own metastore. Catalogs and schemas that are created in one instance were not visible in other instances in the same account. In the account‑scoped model, all instances that you create in the same region share a common metastore.

When you provision a new instance in that region, the instance automatically connects to the shared metadata. Engines such as Spark and Presto in each instance use this common metadata for analytics workflows.

If you create an instance in a different region, {{site.data.keyword.lakehouse_short}} creates a separate metastore for that region.

# Metadata object behavior
{: #account_scope_2}

**Catalogs, data sources, and object storages**

The system now treats catalogs, data sources, and object storages as account‑level resources. As a result, the platform applies the following constraints:

* A catalog name must be unique within the account and region.
* An object storage or bucket name must be unique within the account and region.
* Only one catalog in the account and region can function as the ACL catalog.
* The system continues to provision a QHMM catalog for each instance.

If any engine in any instance references a catalog, you cannot delete that catalog until you remove the engine association.

**Schemas**

Schema constraints depend on the catalog type:

* For Hive, Delta, and Hudi catalogs, schema names must be unique across catalogs in the account and region.
* For Iceberg catalogs, schema names can repeat across different catalogs.

**User experience in the UI**

Users with the appropriate access see the same catalogs, data sources, and storages across all instances in the account.

**Governance model**

The governance model for metadata also moves to the account level. Policies that control access to catalogs, schemas, and tables apply uniformly across all instances in the same account and region.

If your organization previously relied on separate instances to isolate teams, you can achieve similar logical separation by using IAM access groups and applying catalog‑level access policies to each group.

**Metadata service behavior**

The Metadata Service (MDS) provides REST and Thrift interfaces. In the account‑scoped model:

* The Thrift interface uses the Thrift‑HTTP protocol (`https://`) instead of the Thrift‑Binary protocol that is used in instance‑scoped instances.
* All Thrift API calls must include the `account_id` parameter.
* The `catalog` query parameter is required when the APIs involving the Iceberg catalog are invoked.
* The `AccountId` is required for all direct calls to the MDS REST Service (Iceberg catalog and Unity catalog).
* Iceberg operations use the updated REST endpoint `/api/v1/iceberg` instead of `/mds/iceberg`.

IBM watsonx.data automatically configures these parameters for Spark and Presto engines.

**Instance lifecycle behavior**

When you delete an instance, the system does not delete its catalogs, schemas, data sources, or storages. These resources remain accessible to other instances within the same account and region.

Even if you delete every instance in the account, the metadata persists until you explicitly delete it.

# How to identify the scope of an instance
{: #account_scope_3}

**UI**

An instance displays an **Account‑scoped** label in the interface when it operates in account‑scoped mode.

**API**

You can determine the scope of an instance by running the following API:
`GET /v1/instance/{instance_id}/mds`

For more information, see [Account-scope API](https://cloud.ibm.com/apidocs/watsonxdata-infra-services#get-mds).
