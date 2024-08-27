---

copyright:
  years: 2017, 2024
lastupdated: "2024-08-22"

keywords: watsonx.data, spark, emr
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Data Access Service (DAS) endpoint
{: #cas_ep}

Use a DAS endpoint to access {{site.data.keyword.lakehouse_short}} Object Storage storage data to avoid exposing storage credentials by any chance. Your DAS endpoint is:

```bash
https://cas-<region>.lakehouse.appdomain.cloud
```
{: codeblock}

Replace `<region>` with your {{site.data.keyword.lakehouse_short}} instance location. For example:

```bash
https://cas-ussouth.lakehouse.appdomain.cloud
```
{: codeblock}
