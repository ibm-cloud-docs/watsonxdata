---

copyright:
  years: 2022, 2024
lastupdated: "2024-04-03"

keywords: security, data and keys, encrypted

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


# Securing your data in {{site.data.keyword.lakehouse_short}}
{: #mng_data}

Know, how your data is encrypted in {{site.data.keyword.lakehouse_full}} to ensure data security.
{: shortdesc}

The {{site.data.keyword.lakehouse_short}} service has security that is built into all levels of its architecture.

1. Web Console UI, API, Presto, and Hive metastore data in motion is encrypted by using SSL/TLS 1.3.
2. Web Console UI, API, Presto, and Hive metastore authentication and authorization is via IBM Cloud IAM.
3. Presto Kubernetes worker node NVMe SSDs used for local ephemeral RaptorX caching are encrypted by using AES-256.
4. Hive metastore backend database is encrypted by using Key Protect.
5. Backend object storage repositories for internal metadata and 10 GB limited trial bucket are encrypted by using AES-256. Customer Bring-your-own-key (BYOK) via Key Protect and Keep-your-own-key(KYOK)via Hyper Protect Crypto(HPCS) are supported at provision time

## Integrating your data and keys
{: #int_data}

The backend object storage bucket for internal metadata and 10 GB limited trial bucket for watsonx.data can be encrypted with your encryption keys. If you need to control the encryption keys, use IBM Key Protect or Hyper Protect Crypto Services to create, add, and manage encryption keys. Then, you can associate those keys with your watsonx.data deployment to encrypt your buckets.

IBM Key Protect helps you provision encrypted keys for apps across IBM Cloud services. You manage the lifecycle of your keys and benefit as your keys are secured by FIPS140-2 Level 3 certified cloud-based hardware security modules (HSMs) that protects from information theft.

Hyper Protect Crypto Services is a single-tenant, dedicated HSM that is controlled by you. The service is built on FIPS 140-2 Level 4-certified hardware, the highest offered by any cloud provider in the industry. To get started, you need to provision a Key Protect instance or a Hyper Protect Crypto Services instance on your IBM Cloud account.

## Creating or adding a key in the key management service
{: #crea_key}

1. To add a key in Key Protect, go to your instance of Key Protect and generate or enter a key.
2. To add a key in Hyper Protect Crypto Services, navigate to your instance ofHyper Protect Crypto Services(HPCS) and generate a key.

### Regions offered
{: #regn_offr}

The chart that follows, shows which keys can be used in which region.

| **{{site.data.keyword.lakehouse_short}} Regions (IBM)**   |**Key Protect Region Available**  | **HPCS Region Available** |
|---|---|---|
| Dallas (US-South) | US-South | US-South  |
| Washington (US-East) | US-South  |US-East  |
| Frankfurt (EU-DE) | EU-DE  | N/A  |
| London (EU-GB) | EU-DE  | N/A  |
| Tokyo (JP-Tok) | JP-Tok | N/A  |
{: caption="Table 1. Regions - IBM" caption-side="bottom"}

| **{{site.data.keyword.lakehouse_short}} Regions (AWS)**   |**Key Protect Region Available**  | **HPCS Region Available** |
|---|---|---|
| N. Virginia (US-East-1) | US-South | US-East  |
| Oregon (US-West-2) | US-South  |US-South  |
| Frankfurt (EU-Central-1) | EU-DE  | N/A  |
| Tokyo (JP-Tok)| JP-Tok | N/A |
{: caption="Table 1. Regions - AWS" caption-side="bottom"}

## Granting service authorization
{: #gran-auth}

Authorize Key Protect for use with {{site.data.keyword.lakehouse_short}} deployments:
1. Open your IBM Cloud dashboard.
2. From the menu bar, select Manage > Access (IAM).
3. In the side navigation, select Authorizations. Click Create.
4. In the Source service menu, select the service of the deployment. For example, watsonx.data.
5. In the Source service instance menu, select All service instances.
6. In the Target service menu, select Key Protect or Hyper Protect Crypto Services.
7. In the Target service instance menu, select the service instance to authorize.
8. Enable the Reader role. Click Authorize.

## Using the key encryption key
{: #usg-enkey}

After you grant {{site.data.keyword.lakehouse_short}} deployments permission to use your keys, you supply the key name or CRN in Key Protect or Hyper Protect Crypto Services when you provision a deployment. The deployment uses your encryption key to encrypt your data.
