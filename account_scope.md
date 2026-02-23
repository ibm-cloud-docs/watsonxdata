---

copyright:
  years: 2022, 2026
lastupdated: "2026-02-23"

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

# Resource scoping at account level
{: #account_scope}

In {{site.data.keyword.lakehouse_full}}, the resource scope feature allows administrators to restrict visibility and access so that users can see and work with only the resources that belong to their current IBM Cloud account.
{: shortdesc}

An **Account‑scoped** tag that is displayed next to the **Welcome** heading in the {{site.data.keyword.lakehouse_short}} interface indicates that the watsonx.data instance is restricted to a single IBM Cloud account.

In {{site.data.keyword.lakehouse_short}} 2.3.1 release, the **Account‑scoped** mode is available for the {{site.data.keyword.lakehouse_short}} Enterprise edition in Tokyo and Sydney SaaS regions only.
{: note}

The Account‑scoped tag signals that the instance is operating with account‑level resource scope, meaning:

* Users can see and access resources that belong only to the same IBM Cloud account the instance is tied to.
* Projects, catalogs, spaces, and other assets outside that account are not visible or accessible, even if a user has memberships or roles in other accounts.

## Limitations
{: #account_scope_limit}

* Within a single account, the catalog names and bucket names must be unique across all instances in that account. For example, if `test_1` is created as a catalog in account A in any instance, no other catalog in account A can be named `test_1`.

* Within a single account, only one catalog can be designated as the ACL (Access Control List) catalog.

## Identifying scope by using API
{: #account_scope_api}

To identify whether an instance is in account scope or instance scope, use the following API:

`GET /v1/instance/{instance_id}/mds`

Account scope:

```bash
{
    "scope": "account",
    "mds_host": "https://us-south.lakehouse.dev.cloud.ibm.com/",
    "mds_thrift_port": 443,
    "mds_https_port": 443
}
```
{: codeblock}

Instance scope:

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
