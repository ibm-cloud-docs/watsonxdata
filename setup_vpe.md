---

copyright:
  years: 2025
lastupdated: "2025-03-19"

keywords: watsonxdata, vpe

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

# Setting up virtual private endpoints
{: #setup_vpe}

You can configure network endpoints in {{site.data.keyword.lakehouse_short}} to view and manage access to your deployment.
{: shortdesc}

## Procedure
{: #setup_vpe_proc}


1. Log in to the {{site.data.keyword.lakehouse_short}} console.
1. From the navigation menu, select **Configurations**.
1. Click the **Virtual private endpoints** tile. The ***Virtual private endpoints** page opens.
1. Configure the following network endpoints:
    * Public endpoints - Enabled by default
    * Private endpoints - Disabled by default

   Public endpoints can be disabled after you enable the Private endpoints and refresh the engines and services. Private endpoints cannot be disabled after it is enabled.
   {: note}
