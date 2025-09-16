---

copyright:
  years: 2022, 2025
lastupdated: "2025-09-16"

keywords: watsonxdata, sal, auto enrichment

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

# Modifying auto enrichment schedule metadata enrichment jobs
{: #sal_modify_enrichmentrun}

In {{site.data.keyword.lakehouse_full}}, the Semantic automation layer (SAL) automatically triggers metadata enrichment jobs at regular intervals. These jobs enrich metadata for all schema related assets in the Information Knowledge Catalog (IKC). While this ensures timely updates, frequent auto-runs may consume system resources unnecessarily, especially when no changes have occurred.

To optimize performance, users can modify the schedule of these auto generated metadata enrichment jobs through the Software Hub console.

## Before you begin
{: #sal_modify_enrichmentrun1}

You can change the metadata enrichment job schedule in any of these cases:

* The schema assets are updated frequently even when no changes are made.
* The cluster is experiencing performance degradation due to frequent enrichment jobs.
* To align enrichment timing with business hours or only when an update is made.

## Procedure
{: #sal_modify_enrichmentrun2}

1. Log in to Software Hub console.

1. From the navigation menu, select **Projects** to view all available projects.

1. Identify and click on the project associated with the schema that triggers the SAL metadata enrichment job.

1. From the assets tab within the project, click the asset labeled as `SAL_MDE`.

1. Click **Edit enrichment** to modify the job schedule to a preferred interval and save the changes.
