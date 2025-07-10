---

copyright:
  years: 2022, 2025
lastupdated: "2025-07-10"

keywords: Spark, query, server,JDBC, Driver

subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Connecting to Spark query server by using Spark JDBC Driver
{: #dbt_watsonx_connt}

**Applies to** : [Spark engine]{: tag-blue}


You can connect to the Spark query server in the following ways and execute queries to analyze your data.

* [Using DBeaver (JDBC clients)](#dbt_dbvr)
* [Using Java (JDBC Client) code](#dbt_java)
* [Using Python (PyHive JDBC Client)](#dbt_dbvr_Pyth)

## Before you begin
{: #dbt_watsonx_c_bfb}

1. Install watsonx.data.
1. Provision native Spark engine in watsonx.data.
1. Download the JDBC client: `queryserver-jdbc-4.1.0-SNAPSHOT-standalone.jar` from the [Download](https://www.ibm.com/docs/en/watsonx/watsonxdata/2.2.x?topic=wsqs-connecting-spark-query-server-by-using-spark-jdbc-driver#concept_kkt_pzb_5cc__title__2) link.
1. Run the Spark Query Server in Spark engine. To create a new Query Server, see Create a Spark query server.
1. Connection properties - Click the three-dot menu for Query Server, click **Connection Details** and copy the following connection details:
   * Host
   * URI
   * Instance
   * Username
   * Your IBM IAM API key.

## Connecting to Spark query server by using DBeaver (JDBC client)
{: #dbt_dbvr}

To connect to the Spark query server using a JDBC client, such as DBeaver, set up watsonx.data driver in DBeaver.

1. Open DBeaver and in the menu bar click on **Database > Driver Manager**.
1. Search for **Hive**. You can find **Apache Hive 4+** driver under **Hadoop** category.
1. Click **Copy**.
1. Change the name to Spark watsonx.data.
1. Change the following settings :
1. In the **Settings** tab,

1. In the **Libraries** tab - Add the Spark JDBC query server JAR file.

1. Select **Database Navigator**, click on **New Connection** and complete the following steps:
   1. Select the newly created driver.
   1. Click **Connect by** and select **URL**.
   1. Provide the JDBC URL using the following format : `jdbc:hive2://<HOST>:443/default;instance=<INSTANCE>;httpPath=<URI>`.
   1. Select **Authentication**, provide **Username** as your username and your IAM API key as the password.
   1. **Save** and connect to the connection by double-clicking.


## Connecting to Spark query server by using Java (JDBC Client) code
{: #dbt_java}

Ensure your Java CLASSPATH includes the downloaded JDBC driver. For example:

`java -cp queryserver-jdbc-4.1.0-SNAPSHOT-standalone.jar App.java`

You can specify the following parameters and use the following Java code to connect to the Spark query server.

```bash
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.ResultSetMetaData;
import java.sql.Statement;

public class App {
    public static void main(String[] args) throws Exception {
        // Set the below configurations from Connection Details of QueryS Server
        // Exclude having https/http/www, just domain
        String host = "example.com";
        String Instance = "CRN/OR/INSTANCE-ID";
        String uri = "/lakehouse/api/v2/spark_engines/.../query_servers/.../connect/cliservice";
        String user = "EMAIL-ID/OR/USER-ID";
        String apikey = "API-KEY";

        String jdbcUrl = String.format("jdbc:hive2://%s/default;instance=%s;httpPath=%s;", host, Instance, uri);

        // Required if your domain requires SSL certificates
        // This is not required for SaaS, hence comment the below line for SaaS
        // Else, we need provide trust-store path which has the SSL certificates for the host
        jdbcUrl += "sslTrustStore=tech_trust.jks;trustStorePassword=Test@123";

        try {
            // Load the Hive JDBC driver
            Class.forName("com.ibm.wxd.spark.jdbc.QueryServerDriver");

            // Connect to Hive
            Connection con = DriverManager.getConnection(jdbcUrl, user, apikey);
            Statement stmt = con.createStatement();

            System.out.println("Connected to watsonx.data Spark Query Server");

            // Sample query
            String sql = "show databases";

            ResultSet rs = stmt.executeQuery(sql);
            ResultSetMetaData rsmd = rs.getMetaData();
            int columnCount = rsmd.getColumnCount();

            // The column count starts from 1
            for (int i = 1; i <= columnCount; i++ ) {
                System.out.println(rsmd.getColumnName(i));
            }

            // Print result
            while (rs.next()) {
                System.out.println(rs.getString(1)); // Or loop through columns
            }

            // Clean up
            rs.close();
            stmt.close();
            con.close();

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```
{: .codeblock}

## Connecting to Spark query server by using Python (PyHive JDBC Client)
{: #dbt_dbvr_Pyth}

To connect to the Spark query server using a Python program, do the following:


1. Ensure you have Python version 3.12 or below.

1. Install pyHive using pip install PyHive[hive_pure_sasl]==0.7.0.

1. Save the follow in a file like `connect.py`.


   ```bash

   import ssl
   import thrift
   import base64
   from pyhive import hive

   import requests
   import thrift.transport
   import thrift.transport.THttpClient

   import logging
   import contextlib
   from http.client import HTTPConnection


   # Change the following inputs
   class Credentials:
       host = "https://example.ibm.com"
       uri = "/lakehouse/api/v2/spark_engines/.../query_servers/.../connect/cliservice"
       instance_id = "CRN/OR/INSTANCE-ID"
       username = "EMAIL-ID/OR/USER-ID"
       apikey = "API-KEY"


   creds = Credentials()


   def disable_ssl(ctx):
       ctx.check_hostname = False
       ctx.verify_mode = ssl.CERT_NONE

       ssl.SSLContext.verify_mode = property(lambda self: ssl.CERT_NONE, lambda self, newval: None)


   def get_access_token(apikey):
       try:
           headers = {
               'Content-Type': 'application/x-www-form-urlencoded',
               'Accept': 'application/json',
           }

           data = {
               'grant_type': 'urn:ibm:params:oauth:grant-type:apikey',
               'apikey': apikey,
           }

           response = requests.post('https://iam.cloud.ibm.com/identity/token', headers=headers, data=data)
           return response.json()['access_token']
       except Exception as inst:
           print('Error in getting access token')
           print(inst)
           exit

   ctx = ssl.create_default_context()

   ## If you require to disable SSL, uncomment the below line
   # disable_ssl(ctx)

   transport = thrift.transport.THttpClient.THttpClient(
       uri_or_host="{host}:{port}{uri}".format(
           host=creds.host, uri= creds.uri, port=443,
       ),
       ssl_context=ctx,
   )

   headers = {
       "AuthInstanceId": creds.instance_id
   }

   if creds.instance_id.isdigit():
       # Software installation
       headers["Authorization"] =  "ZenApiKey " + base64.b64encode(f"{creds.username}:{creds.apikey}".encode('utf-8')).decode('utf-8')
   else:
       # Cloud installation
       headers["Authorization"] = "Bearer {}".format(get_access_token(creds.apikey))

   transport.setCustomHeaders(headers)

   cursor = hive.connect(thrift_transport=transport).cursor()
   print("Connected to Spark Query Server")

   cursor.execute('show databases')
   print(cursor.fetchall())

   cursor.close()

   ```
   {: .codeblock}


4. Run using `python connect.py`.
