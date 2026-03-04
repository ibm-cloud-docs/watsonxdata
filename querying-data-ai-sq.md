---

copyright:
  years: 2022, 2025
lastupdated: "2026-03-04"

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

# System requirements
{: #squerying-data-ai-sq}

**Software prerequisites**
{: #squerying-data-ai-sp}

Before you begin, ensure that your system meets the following requirements:

| Component | Requirement | Notes |
|-----------|-------------|-------|
| Python | Version 3.11 or later | [Download Python](https://www.python.org/downloads/) |
| Package manager | uv | [Install uv](https://github.com/astral-sh/uv) |
| IBM Cloud account | Active account | [Register for IBM Cloud](https://cloud.ibm.com/registration) |
{: caption="System requirements" caption-side="bottom"}

**IBM {{site.data.keyword.lakehouse_short}} requirements**
{: #squerying-data-ai-reqi}

You must have access to the following IBM {{site.data.keyword.lakehouse_short}} resources:

- **{{site.data.keyword.lakehouse_short}} instance**: A provisioned and running instance

   - [Provision a lite plan instance](/docs/watsonxdata?topic=watsonxdata-tutorial_prov_lite_1) and [Provision an enterprice plan instance](/docs/watsonxdata?topic=watsonxdata-getting-started_1)

   - [Set up {{site.data.keyword.lakehouse_short}} lite plan](/docs/watsonxdata?topic=watsonxdata-tutorial_hp_intro)

- **IBM Cloud API key**: An API key with appropriate permissions

   - [Create an API key](https://cloud.ibm.com/iam/apikeys)

**Required configuration information**
{: #squerying-data-ai-cnf}

Collect the following information before installation:

- **Base URL**: The URL of your {{site.data.keyword.lakehouse_short}} instance
   - Format: `"https://your-instance.lakehouse.cloud.ibm.com/lakehouse/api/lakehouse/api`

- **Instance CRN**: The Cloud Resource Name of your instance. To find CRN, refer [Getting connection information](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-get_connection).

   - Format: `crn:v1:bluemix:public:lakehouse:us-south/a/...`

   - To locate your Instance CRN:

    1. Log in to the {{site.data.keyword.lakehouse_short}} console.
    2. On the **Instance details** or **Configuration** page, locate the **CRN** field in the details section.
    3. Click the copy icon next to the CRN to copy it to your clipboard.

- **IAM API Key**: Your IBM Cloud API key with {{site.data.keyword.lakehouse_short}} access permissions.
