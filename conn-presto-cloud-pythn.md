---

copyright:
  years: 2022, 2024
lastupdated: "2024-01-31"

keywords: watsonxdata, watsonx.data, presto, python client, cloud

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

# Connecting to Presto server using Python client
{: #con-presto-cloud-pythn}

Presto CLI provides a terminal-based interactive shell to run queries.
{: shortdesc}

Complete the following steps to connect to Presto engine in {{site.data.keyword.lakehouse_full}} instance on {{site.data.keyword.cloud_notm}} through a Python client or application.

## Getting the Presto engine hostname and port details
{: #get-host-port2}

1. Log in to the {{site.data.keyword.lakehouse_short}} service instance in {{site.data.keyword.cloud_notm}}.

2. Go to **Infrastructure Manager** and click **List view**.

3. In the **Engines** tab, click the engine name for which you need the hostname and port details.

4. Under the **Host** label, click the **Copy to clipboard** icon to copy the host details.

5. Copy the host details to a notepad.

## Getting the IBM API key or IBM IAM token
{: #get-api-iam-token2}

Use either IBM API key or IBM IAM token according to your requirement.

### Getting IBM API Key
{: #get-ibmapi-key2}

1. Log in to the [IBM Cloud console](http://test.cloud.ibm.com/).

2. In the navigation bar, click **Manage** and select **Access (IAM)**.

3. Click **API keys** in the left navigation bar.

4. Click **Create +**.

5. In **Create IBM Cloud API key** window, enter a name for your API key and enter the appropriate description for the key. For example, `ibmiamtoken testing`

6. Click **Create**. A window with message **API key successfully created** displays.

7. Click **Download** to save the API key to your local machine.

8. Open the downloaded file and copy the API key to a notepad file.

### Getting IBM Access Management (IAM) token
{: #get-ibmiam-token2}

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
{: #conn-to-prestoeng2}

1. Download and install the [presto-python-client](https://prestodb.io/docs/current/installation/jdbc.html) on the client machine by using the package installer for Python (pip3).

2. Use the DBAPI interface to query Presto:

   ```bash
   import prestodb
   conn=prestodb.dbapi.connect(
   host=<host_name>,
   port=443,
   user='admin',
   catalog=<catalog_name>,
   schema=<schema_name>,
   http_scheme='https',
   auth=prestodb.auth.BasicAuthentication("admin","<pwd>")
   )
   conn._http_session.verify = 'ingress.pem'
   cur = conn.cursor()
   cur.execute('SELECT * FROM system.runtime.queries')
   rows = cur.fetchall()
   print(rows)
   ```
   {: codeblock}

   The command queries the `system.runtime.nodes` system tables that show the nodes in the Presto cluster.
   The DBAPI implementation in `prestodb.dbapi` provides methods to retrieve few rows. For example, `Cursorfetchone()` or `Cursor.fetchmany()`. By default `Cursor.fetchmany()` fetches one row. Set `prestodb.dbapi.Cursor.arraysize` accordingly.
   {: note}

4. Compile and run the command.
