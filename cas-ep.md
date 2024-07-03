---

copyright:
  years: 2017, 2024
lastupdated: "2024-07-03"

keywords: watsonx.data, spark, emr
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Content Aware Storage (CAS) endpoint
{: #cas_ep}

Use a CAS endpoint to access {{site.data.keyword.lakehouse_short}} Object Storage bucket data to avoid exposing bucket credentials by any chance. Your CAS endpoint is:

```bash
https://cas-<region>.lakehouse.appdomain.cloud
```
{: codeblock}

Replace `<region>` with your {{site.data.keyword.lakehouse_short}} instance location. For example:

```bash
https://cas-ussouth.lakehouse.appdomain.cloud
```
{: codeblock}
