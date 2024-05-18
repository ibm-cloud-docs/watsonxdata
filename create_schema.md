---

copyright:
  years: 2022, 2024
lastupdated: "2024-05-16"

keywords: watsonxdata, schema

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

# Creating schema
{: #create_schema}

You can create schema from the **Data manager** page by using the web console.
{: shortdesc}

1. Log in to {{site.data.keyword.lakehouse_full}} console.
1. Select **Data manager** from the navigation menu.
1. Select the engine from the **Engine** menu. The catalogs that are associated with the selected engine are displayed.
1. Click the **Create** drop-down and select **Create schema**.
    1. In the **Create schema** form, select the catalog and enter schema name.
    1. Click **Create**. The schema is created under the selected catalog.

Do not use special character such as question mark (?) or asterisk (*) in schema name.
{: note}

Make sure to fulfil the [requirements](watsonxdata?topic=watsonxdata-reg_bucket#important_info) before creating a schema against a registed bucket. Otherwise, the system returns the following error message.

```text
Failed to create schema. Try the following measures to resolve the error:
 - Ensure you have the required permissions.
 - Enter the correct credentials.
 - Enter the correct storage path for the bucket.
 - Ensure the bucket is registered with watsonx.data and then retry.
```
{: screen}
