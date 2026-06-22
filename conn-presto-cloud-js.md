---
copyright:
  years: 2024
lastupdated: "2024-01-26"

keywords: watsonxdata, watsonx.data, presto, javascript client, rest api, cloud

subcollection: watsonxdata
---

{:javascript: #javascript .ph data-hd-programlang='javascript'}
{:java: #java .ph data-hd-programlang='java'}
{:ruby: #ruby .ph data-hd-programlang='ruby'}
{:php: #php .ph data-hd-programlang='php'}
{:python: #python .ph data-hd-programlang='python'}
{:typescript: #typescript .ph data-hd-programlang='typescript'}
{:external: target="\_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:video: .video}

# Connecting to Presto server using JavaScript Client
{: #conn-presto-cloud-js}

Presto JS Client connects to Presto via the Presto's REST API to run queries.
{: shortdesc}

Complete the following steps to connect to Presto engine in {{site.data.keyword.lakehouse_full}} instance on {{site.data.keyword.cloud_notm}} through a JavaScript client.

## Getting the Presto engine hostname and port details
{: #get-host-port1}

1. Log in to the {{site.data.keyword.lakehouse_short}} service instance in {{site.data.keyword.cloud_notm}}.

2. Go to **Infrastructure Manager** and click **List view**.

3. In the **Engines** tab, click the engine name for which you need the hostname and port details.

4. Under the **Host** label, click the **Copy to clipboard** icon to copy the host details.

5. Copy the host details to a notepad.

## Getting the IBM API key or IBM IAM token
{: #get-api-iam-toke1}

Use either IBM API key or IBM IAM token according to your requirement.

### Getting IBM API Key
{: #get-ibmapi-key1}

1. Log in to the [IBM Cloud console](http://test.cloud.ibm.com/).

2. In the navigation bar, click **Manage** and select **Access (IAM)**.

3. Click **API keys** in the left navigation bar.

4. Click **Create +**.

5. In **Create IBM Cloud API key** window, enter a name for your API key and enter the appropriate description for the key. For example, `ibmiamtoken testing`

6. Click **Create**. A window with message **API key successfully created** displays.

7. Click **Download** to save the API key to your local machine.

8. Open the downloaded file and copy the API key to a notepad file.

### Getting IBM Access Management (IAM) token
{: #get-ibmiam-token1}

1. Call the REST endpoint in IAM to get the IAM token.

2. Replace `<your-api-key>` with your IBM API key.

   ```bash
   curl -X POST \
   'https://iam.cloud.ibm.com/identity/token' \
   --header "Content-Type: application/x-www-form-urlencoded" \
   --data-urlencode "grant_type=urn:ibm:params:oauth:grant-type:apikey" \
   --data-urlencode "apikey=<your-api-key>"
   ```
   {: codeblock}

## Connecting to Presto engine
{: #conn-to-prestoeng3}

1. Download and install the [presto-js-client](https://www.npmjs.com/package/@prestodb/presto-js-client) package with npm.

   ```sh
   npm install @prestodb/presto-js-client
   ```
   {: codeblock}

2. Import the `PrestoClient` class from @prestodb/presto-js-client and create a new instance by passing the connection parameters. Then you can use the `query` method to retrieve data.

   ```typescript
   import PrestoClient from "@prestodb/presto-js-client";

   const client = PrestoClient({
     basicAuthentication: {
       user: "ibmapikey_<EMAIL_ID>",
       password: <API_KEY>,
     },
     host: <HOST>,
     port: <PORT>,
     user: "admin",
   });

   const query = `SELECT * FROM catalog.schema.table`;
   try {
     const prestoQuery = await client.query(query);
     const results = prestoQuery.data;
   } catch (error) {
     if (error instanceof PrestoError) {
       console.error(error.errorCode);
     }
   }
   ```
   {: codeblock}
