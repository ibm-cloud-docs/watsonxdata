---

copyright:
  years: 2022, 2024
lastupdated: "2024-08-27"

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
1. From the navigation menu, select **Data manager**, click **Browse data**.
1. Select the engine from the **Engine** drop-down. Catalogs that are associated with the selected engine are listed.

1. There are two ways to create a schema. Select the required option:

   Option 1: To create a schema under any catalog, do the following steps:

   a. Click **Create**.

   b. Click **Create schema**. The **Create schema** page opens.

   c. Go to step 5.

   Option 2: To import file to a particular schema under the catalog, do the following steps:

   a. Select a catalog where you want to create a schema.

   b. Click the overflow menu of the selected catalog and select **Create schema**. The **Create schema** page opens.

   c. Go to step 5.

1. In the **Create schema** form, select the catalog. Enter schema name.

1. Click **Create**. The schema is created under the selected catalog.

   When you name a schema:

   a. Do not wrap the schema name in quotation marks. (Example: Use test instead of “test”.)

   b. Do not use semicolon [;], colon [:], single quotation mark ['], or double quotation mark ["] in the schema name.

   c. Do not use leading space in the schema name.

   d. Do not use special character such as question mark (?) or asterisk (*) in schema name.

Make sure to fulfil the [requirements]({{site.data.keyword.ref-reg_bucket-link}}) before creating a schema against a registed storage. Otherwise, the system returns the following error message.

```text
Failed to create schema. Try the following measures to resolve the error:
 - Ensure you have the required permissions.
 - Enter the correct credentials.
 - Enter the correct storage path for the storage.
 - Ensure the storage is registered with watsonx.data and then retry.
```
{: screen}
