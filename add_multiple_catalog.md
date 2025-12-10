---

copyright:
  years: 2022, 2025
lastupdated: "2025-12-02"

keywords: lakehouse, watsonx.data, query optimizer, install

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

# Adding multiple Apache Iceberg catalogs to a single storage
{: #muticatlog}

This feature is available only in the watsonx.data Lite instance.
{: important}

You can add multiple Apache Iceberg catalogs to a single storage, as long as all catalogs use Apache Iceberg.

You cannot share a storage between Iceberg and non-Iceberg catalogs.
{: note}

## Before you begin
{: #muticatlog1}

- Make sure that you have specified the base path for the first Apache Iceberg catalog during the storage configuration. For more information, see [Adding storage](/docs/watsonxdata?topic=watsonxdata-reg_bucket).

## Procedure
{: #muticatlog2}

1. Hover over the **Storage** where you want to add a new Apache Iceberg catalog.
2. Click the **Add Catalog** icon.
3. In the **Add Catalog** window, enter the catalog name and base path.

You cannot add catalogs with overlapping base paths under the same bucket, as the system does not permit it.
{: note}

4. Click **Add**.
