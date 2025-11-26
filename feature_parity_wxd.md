---

copyright:
  years: 2022, 2025
lastupdated: "2025-11-26"

keywords: lakehouse, milvus, watsonx.data

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

# Cloud availability of IBM® {{site.data.keyword.lakehouse_short}} and AstraDB
{: #feature_parity_wxd}

{{site.data.keyword.lakehouse_full}} can be deployed as a managed software as a service (SaaS) or installed on premises. As new features are added on each deployment's release cycle, it is important that you understand which features are available in a deployment, so you can make informed decisions based on your business’s requirements.

Stay up to date with the latest features through [Release notes for {{site.data.keyword.lakehouse_short}}](/docs/watsonxdata?topic=release).

This topic covers details for IBM-managed watsonx.data and AstraDB instances in IBM Cloud, Amazon Web Services (AWS), Microsoft Azure, and Google Cloud Platform (GCP).

## Cloud availability
{: #cloudavilbilty}

The cloud availability is based on the features that you can handle through {{site.data.keyword.lakehouse_short}}'s user interface.

For more information on how each deployment is classified based on its support for specific features and capabilities, refer to [Platform comparison: AstraDB versus IBM® {{site.data.keyword.lakehouse_short}}](/docs/watsonxdata?topic=watsonxdata-wxd_plfrm_dplmnt_cmpar#wxd_plfrm_dplmnt2).

### IBM Cloud availability
{: #ibm_cloud}

| Region | Sub-region | Name | AstraDB serverless | watsonx.data | watsonx.data premium |
| --- | --- | --- | --- | --- | --- |
| NA | Dallas | us-south | ❌ | ✅ | ❌ |
| NA | Washington | us-east | ❌ | ✅ | ❌ |
| NA | Toronto | ca-tor | ❌ | ✅ | ✅ |
| NA | Montreal | ca-mon | ❌ | ❌ | ❌ |
| EMEA | Frankfurt | eu-de | ❌ | ✅ | ❌ |
| EMEA | London | eu-gb | ❌ | ✅ | ❌ |
| EMEA | Madrid | eu-es | ❌ | ❌ | ❌ |
| APAC | Tokyo, Japan | jp-tok | ❌ | ✅ | ❌ |
| APAC | Osaka, Japan | jp-osa | ❌ | ❌ | ❌ |
| APAC | Sydney | au-syd | ❌ | ✅ | ❌ |
| SA | Sao Paulo | br-sao | ❌ | ❌ | ❌ |
{: caption="IBM Cloud availability" caption-side="bottom"}

### AWS availability
{: #aws_avlty}

| Region | Sub-region | Name | AstraDB serverless | watsonx.data | watsonx.data premium |
|---|---|---|---|---|---|
| NA | N. Virgina | us-east-1 | ✅ | ✅ | ❌ |
| NA | Oregon | us-west-2 | ✅ | ❌ | ❌ |
| NA | Ohio | us-east-2 | ✅ | ❌ | ❌ |
| NA | Montréal, Québec | ca-central-1 | ✅ | ❌ | ❌ |
| EMEA | Frankfurt | eu-central-1 | ✅ | ✅ | ❌ |
| EMEA | Ireland | eu-west-1 | ✅ | ❌ | ❌ |
| EMEA | London | eu-west-2 | ✅ | ❌ |❌|
| EMEA | UAE | me-central-1 | ❌ | ❌ |❌|
| APAC | Singapore | ap-southeast-1 | ✅ |✅ |❌|
| APAC | Mumbai, India | ap-south-1 | ✅ | ✅ |❌|
| APAC | Tokyo, Japan | ap-northeast-1 | ✅ |❌|❌|
| APAC | Osaka, Japan | ap-northeast-2 | ✅ | ❌ |❌|
| APAC | Sydney | ap-southeast-2 | ✅ | ✅ |❌|
| APAC | Hong Kong | ap-east-1 | ❌ | ❌ |❌|
| SA | Sao Paulo | sa-east-1 | ❌ | ❌ |❌|
{: caption="AWS availability" caption-side="bottom"}

### Microsoft Azure availability
{: #microsft_azure_avlty}

| Region | Sub-region | Name | AstraDB serverless | watsonx.data | watsonx.data premium |
| --- | --- | --- | --- | --- | --- |
|NA|Washington|westus2|✅|❌|❌|
|NA|Virginia|eastus|✅|❌|❌|
|NA|Virginia|eastus2|❌|❌|❌|
|NA|Iowa|centralus|❌|❌|❌|
|NA|Toronto|canadacentral|✅|❌|❌|
|NA|Arizona|westus3|❌|❌|❌|
|EMEA|Netherlands|westeurope|✅|❌|❌|
|EMEA|Ireland|northeurope|✅|❌|❌|
|EMEA|Paris (France)|francecentral|❌|❌|❌|
|APAC|New South Wales (Australia)|australiaeast|✅|❌|❌|
|APAC|Central India (Pune)|centralindia|❌|❌|❌|
|APAC|Victoria (Australia)|australiasoutheast|✅|❌|❌|
|SA|Sao Paulo State|brazilsouth|❌|❌|❌|
{: caption="RMicrosoft Azure availability" caption-side="bottom"}

### Google Cloud Platform
{: #google_cld_plfrm}

| Region | Sub-region | Name | AstraDB serverless | watsonx.data | watsonx.data premium |
| --- | --- | --- | --- | --- | --- |
| NA | Moncks Corner, South Carolina | us-east1 | ✅ | ❌ |❌|
| NA | Ashburn, Virginia | us-east4 | ✅ | ❌ |❌|
| NA | The Dalles, Oregon | us-west1 | ✅ | ❌ |❌|
| NA | Montreal, Quebec | northamerica-northeast1 | ✅ | ❌ |❌|
| NA | Council Bluffs, Iowa | us-central1 | ✅ | ❌ |❌|
| NA | Las Vegas, Nevada | us-west4 | ❌ | ❌ |❌|
| NA | Toronto, Canada | northamerica-northeast2 | ❌ | ❌ |❌|
| EMEA | St. Ghislain, Belgium | europe-west1 | ✅ | ❌ |❌|
| EMEA | London, England | europe-west2 | ❌ | ❌ |❌|
| EMEA | Netherlands | europe-west4 | ❌ | ❌ |❌|
| EMEA | Frankfurt | europe-west3 | ❌ | ❌ |❌|
| EMEA | Hamina, Finland | europe-north1 | ✅ | ❌ |❌|
| EMEA | Eemshaven, Netherlands | europe-west4 | ✅ | ❌ |❌|
| APAC | Mumbai, India | asia-south1 | ❌ | ❌ |❌|
| APAC | Tokyo, Japan | asia-northeast1 | ❌ | ❌ |❌|
| APAC | Sydney, Australia | australia-southeast1 | ✅ | ❌ |❌|
| APAC | Osaka | asia-northeast2 | ❌ | ❌ |❌|
| APAC | Hong Kong | asia-east2 | ✅ | ❌ |❌|
| APAC | Changhua County, Taiwan | asia-east1 | ✅ | ❌ |❌|
{: caption="Google Cloud Platform" caption-side="bottom"}
