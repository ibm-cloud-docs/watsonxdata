---

copyright:
  years: 2022, 2025
lastupdated: "2025-03-06"

keywords: lakehouse, metadata, service, mds, max pool, watsonx.data

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

# Customizing max pool size in Metadata Service
{: #mdcustm}

You can specify the maximum number of connections in a connection pool that is used by the Metadata Service (MDS).
{: shortdesc}

## Procedure
{: #mdcustm_mx}

To specify the maximum number of connections in a connection pool, use the `MDS_DB_CONNECTION_MAX_POOL_SIZE` property. The value is set to 10 by default.
Following is the command:

   ```bash
   oc patch wxd/lakehouse --type=merge -n cpd-instance -p "{ "spec": {
             "MDS_DB_CONNECTION_MAX_POOL_SIZE":"<value>"
  } }"
   ```
   {: codeblock}

To set the value, in CPD/{{site.data.keyword.lakehouse_full}} on-prem you need to log in as CPD admin. For {{site.data.keyword.lakehouse_short}} SaaS, reach out to the SRE or the Support team.

For more information about customizing watsonx.data components, see [Customizing {{site.data.keyword.lakehouse_short}} components](https://www.ibm.com/docs/en/software-hub/5.1.x?topic=components-customizing-in-watsonxdata).
