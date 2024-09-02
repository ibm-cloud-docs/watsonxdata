---

copyright:
  years: 2022, 2024
lastupdated: "2024-09-02"

keywords: watsonxdata, troubleshoot, case sensitivity

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

## Re-enrichment not reflecting glossary updates in semantic automation
{: #ts_sal_gls_enrch}

### What’s happening
{: #ts_salglsenrch1}

Updating a watsonx.data glossary in semantic automation does not impact previously enriched watsonx.data tables.

### Why it’s happening
{: #ts_salglsenrch2}

Metadata enrichment run determines that the data has already been enriched and skips re-evaluation. Therefore, subsequent metadata enrichment runs immediately gets terminated due to the existing enriched state.

### How to fix it
{: #ts_salglsenrch3}

Try the following to resolve the issue:

1. Locate the corresponding Semantic automation project in CPD for the affected watsonx.data table.

   ```bash
   ???
   ```
   {: codeblock}

1. Delete the metadata enrichment asset associated with the Semantic automation project. This will also delete the metadata enrichment job.

   ```bash
   ???
   ```
   {: codeblock}

1. Return to watsonx.data and re-enrich the table. The updated glossary terms will now be used for the new enrichment process.

   ```bash
   ???
   ```
   {: codeblock}
