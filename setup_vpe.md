---

copyright:
  years: 2025
lastupdated: "2025-03-22"

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
{:restriction: .restriction}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:video: .video}

# Setting up virtual private endpoints
{: #setup_vpe}

You can configure network endpoints in {{site.data.keyword.lakehouse_short}} to view and manage access to your deployment.
{: shortdesc}

Private endpoints are not supported for Lite plans. Private endpoints are supported only in `ca-tor` and `au-syd` regions.
{: important}

## Procedure
{: #setup_vpe_proc}


1. Log in to the {{site.data.keyword.lakehouse_short}} console.
1. From the navigation menu, select **Configurations**.
1. Click the **Virtual private endpoints** tile. The **Virtual private endpoints** page opens. You can configure the following network endpoints:
    * Public endpoints - Enabled by default
    * Private endpoints - Disabled by default
1. To enable private endpoints for your deployment, click **Private endpoints** and refresh the engines and services.

   You cannot disable the private endpoints after it is enabled.
   {: note}

1. Optional: To disable the public endpoints, click **Public endpoints**.

   You can disable the public endpoints only after you enable the private endpoints and refresh the engines and services.
   {: restriction}

## Result
{: #setup_vpe_res}

The **Virtual Private Endpoint** is displayed in the **Private endpoints** table when you successfully enable the private endpoints for your deployment.

## What to do next
{: #setup_vpe_next}

You can create a Virtual private endpoint gateway to connect to a {{site.data.keyword.lakehouse_short}} instance. For more information see [Creating VPE gateways](/docs/vpc?topic=vpc-ordering-endpoint-gateway).
