---

copyright:
  years: 2022, 2026
lastupdated: "2026-02-24"

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

# Component scoping at account level
{: #account_scope}

In {{site.data.keyword.lakehouse_full}}, the account scoping feature enables you to retain the account level components such as catalogs, databases, buckets, and their metadata properties independently of individual instances.
{: shortdesc}

In {{site.data.keyword.lakehouse_short}} 2.3.1 release, the **Account‑scoped** mode is available for the {{site.data.keyword.lakehouse_short}} Enterprise edition in Tokyo and Sydney SaaS regions only.
{: note}

An **Account‑scoped** tag that is displayed next to the **Welcome** heading in the {{site.data.keyword.lakehouse_short}} interface indicates that the watsonx.data instance is restricted to a single IBM Cloud account. Users can see and access resources that belong only to the same IBM Cloud account the instance is tied to.

When an instance is deleted in {{site.data.keyword.lakehouse_short}}, the account level components such as catalogs, databases, and buckets are not removed. These componenets remain fully accessible to any other instance within the same account and region. However, if a catalog-bucket pair is assigned to an engine within any instance in the same account, that catalog cannot be deleted until the association is removed.

For account-scoped resources, only one catalog can be designated as the ACL (Access Control List) catalog. The catalog names and bucket names must also be unique across all instances in that account. For example, if a catalog named `test_1` exists in any instance within account A, no other catalog in that account can be created with the same name.

**Requirements**:

* The `account_id` is mandatory for all Thrift API calls made to the MDS Thrift Service over HTTP.
* The `AccountId` is required for all direct calls to the MDS REST Service (Iceberg Catalog and Unity Catalog).

The endpoint for Iceberg operations is updated from `/mds/iceberg` to `/api/v1/iceberg`.
{: note}

## Identifying scope by using API
{: #account_scope_api}

To identify whether an instance is in account scope or instance scope, use the following API:

`GET /v1/instance/{instance_id}/mds`

**Account scope**:

```bash
{
    "scope": "account",
    "mds_host": "https://us-south.lakehouse.dev.cloud.ibm.com/",
    "mds_thrift_port": 443,
    "mds_https_port": 443
}
```
{: codeblock}

**Instance scope**:

```bash
{
    "scope": "instance",
    "mds_host": "16375c7a-cd6e-495a-89f9-cdc05e66b3b9.cs2bek7w0ooo0psc7qdg.lakehouse.dev.ibmappdomain.cloud",
    "mds_thrift_port": 32176,
    "mds_https_port": 32616
}
```
{: codeblock}

For more information, see [Account-scope API](https://cloud.ibm.com/apidocs/watsonxdata-infra-services#get-mds).
