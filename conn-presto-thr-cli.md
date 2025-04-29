---

copyright:
  years: 2022, 2025
lastupdated: "2025-04-29"

keywords: lakehouse, watsonx.data, presto, cli

subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Connecting to Presto server
{: #con-presto-serv}

Presto CLI provides a terminal-based interactive shell to run queries.
{: shortdesc}

In {{site.data.keyword.lakehouse_full}}, you can connect to the Presto server in multiple ways based on the platform and utilities you are using. See the following sections for more details:

- [Connecting to Presto engine using Presto CLI (Remote)](#conn-to-prestoeng)
- [Connecting to Presto engine using Java/JDBC](#conn-to-prestjava)
- [Connecting to Presto engine using Python scripts](#conn-to-prestpython)

You must specify the location when you create schema using CLI. For example,
`location = s3a://<storage-name>/`
{: note}

## Pre-requisites
{: #con-presto-prereq}

### Getting the Presto engine hostname and port details
{: #get-host-port}

1. Log in to {{site.data.keyword.lakehouse_short}} web console.

2. Go to **Infrastructure Manager** and click **List view**.

3. In the **Engines** tab, click the engine name for which you need the hostname and port details.

4. Under the **Host** label, click the **Copy to clipboard** icon to copy the host details.

5. Copy the host details to a notepad.


- [Getting the IBM API key or IBM IAM token](#get-api-iam-token)
- [Getting IBM API Key](#get-ibmapi-key)
- [Getting IBM Access Management (IAM) token](#get-ibmiam-token)

### Getting the IBM API key or IBM IAM token
{: #get-api-iam-token}

Use either IBM API key or IBM IAM token according to your requirement.

It is recommended to use IAM token for stress workload.
{: tip}

#### Getting IBM API Key
{: #get-ibmapi-key}

If you enabled `External Identity Interactions Limited` feature, and using API keys to communicate with {{site.data.keyword.lakehouse_short}}, you must create the API key from the account where the {{site.data.keyword.lakehouse_short}} is provisonined.
{: note}


1. Log in to the [IBM Cloud console](http://cloud.ibm.com/).

2. In the navigation bar, click **Manage** and select **Access (IAM)**.

3. Click **API keys** in the left navigation bar.

4. Click **Create +**.

5. In the **Create IBM Cloud API key** window, enter a name for your API key and enter the appropriate description for the key. For example, `ibmlhtoken testing`

6. Click **Create**. A window with message **API key successfully created** displays.

7. Click **Download** to save the API key to your local machine.

8. Open the downloaded file and copy the API key to a notepad file.

#### Getting IBM Access Management (IAM) token
{: #get-ibmiam-token}

1. Call the REST endpoint in IAM to get the IAM token.

2. Replace `<your-api-key>` with your IBM API key.

   ```bash
   curl -X POST 'https://iam.cloud.ibm.com/identity/token' -H 'Content-Type: application/x-www-form-urlencoded' -d 'grant_type=urn:ibm:params:oauth:grant-type:apikey&apikey=MY_APIKEY'
   ```
   {: codeblock}

## Connecting to Presto engine through Presto CLI (Remote)
{: #conn-to-prestoeng}

1. Download the Presto executable `jar` from [https://prestodb.io/getting-started/](https://prestodb.io/getting-started/)

2. Rename the downloaded file as **presto**. Make it executable with `chmod +x` and run it.

3. To check whether Presto CLI is installed, run `./presto --version`. Presto cli version displays. For example, `Presto CLI 0.281-cfbc6eb`

4. Run the following commands in the system where Presto CLI is installed. You can use one of the following methods to authenticate to Presto:

   * **Using username and password** : To do that run the following command:

      - If you are using API key, run the following command:

          ```bash
          ./presto --server <https://Prestoengine host details> --catalog iceberg_data --schema default --user ibmlhapikey_<your-username> --password
          ```
          {: codeblock}

      - If you are using IBM IAM token, run the following command:

          ```bash
          ./presto --server <https://Prestoengine host details> --catalog iceberg_data --schema default --user ibmlhtoken_<your-username> --password
          ```
          {: codeblock}

      `<your-username>` is optional if you have multiple connections with different users and want to differentiate them.
      {: note}

      Enter your IBM API key or IBM IAM token at the prompt.

   * **JWT token** : The JWT method of authentication is available by default from 2.1.2 onwards. Run the following command to connect to presto using JWT token:

   To use this method of authentication for the previous versions of {{site.data.keyword.lakehouse_short}} (prior to 2.1.2 release), contact IBM support and enable the feature.
   {: note}

       ```bash
       ./presto --server <https://Prestoengine host details> --catalog iceberg_data --schema default --access-token <ACCESS_TOKEN>
       ```
       {: codeblock}

      To generate `<ACCESS_TOKEN>`, use one of the following methods:

      * Getting IBM Access Management (IAM) token, see [(IAM) token](/docs/watsonxdata?topic=watsonxdata-con-presto-serv#get-ibmiam-token).

      * Get `<ACCESS_TOKEN>` by using the following command:


       ```bash
       curl --location 'https://us-south.lakehouse.dev.cloud.ibm.com/lakehouse/api/v2/auth/authenticate/' \
       --header 'Content-Type: application/json' \
       --data-raw '{
        "username": "ibmlhtoken_<user-name>",
        "password": "<IAM_TOKEN>",
        "instance_id": "<instance_id>",
        "instance_name": ""
       }'
       ```
       {: codeblock}

       `<IAM_TOKEN>` : Specify the token generated from [(IAM) token](/docs/watsonxdata?topic=watsonxdata-con-presto-serv#get-ibmiam-token).

       `<user-name>` : Specify the email id.

       `<instance_id>` : Specify the instance CRN.

6. At the Presto prompt, type `show catalogs;`. The catalog list appears. Now you are connected to Presto engine in {{site.data.keyword.lakehouse_short}} through Presto CLI.

   ```bash
   presto:default> show catalogs;
   Catalog
   --------------
   iceberg_data
   jmx
   system
   tpcds
   tpch
   (5 rows)
   ```
   {: codeblock}


## Connecting to Presto engine using Java/JDBC
{: #conn-to-prestjava}

1. Download and install the [latest JDBC drivers](https://prestodb.io/docs/current/clients/java.html) on the client machine.

2. Add the downloaded `jar` file to the class path of your Java application.

3. Get the API key.

   Use `ibmlhapikey` as the username and API key as password. For more information, see [Getting IBM API Key](#get-ibmapi-key).

4. Get the hostname and port. For more information, see [Getting the Presto engine hostname and port details](#get-host-port).

5. Create a Java application by using JDBC interface. Following is an example for Java snippet:


   ```bash

   import java.sql.Connection;
   import java.sql.DriverManager;
   import java.sql.ResultSet;
   import java.sql.Statement;
   import java.util.Properties;

   public class PrestoJdbcSample
   {
       public static void main(String[] args) throws Exception
       {
           /*
            * example of fetching the location and credentials needed to connect, from
            * environment variables
            */
           String username = System.getenv("ENG_USERNAME");
           String password = System.getenv("ENG_PASSWORD");
           String hostname = System.getenv("ENG_HOST");
           String portnumber = System.getenv("ENG_PORT");
           String presto_url = "jdbc:presto://" + hostname + ":" + portnumber;
           Connection connection = null;
           Statement statement = null;
           ResultSet resultSet = null;
           try
           {
               /* load the Presto JDBC Driver class  */
               String driverClass = "com.facebook.presto.jdbc.PrestoDriver";
               Class.forName(driverClass);
               /* Set the connection properties */
               Properties properties = new Properties();
               properties.setProperty("user", username);
               properties.setProperty("password", password);
               properties.setProperty("SSL", "true");
               /* Connect */
               connection = DriverManager.getConnection(presto_url, properties);
               /* Issue a Query */
               String query = "SELECT * FROM tpch.tiny.customer LIMIT 10";
               statement = connection.createStatement();
               resultSet = statement.executeQuery(query);
               /* iterate through the results */
               while (resultSet.next())
               {
                   String phone = resultSet.getString("phone");
                   String name = resultSet.getString("name");
                   System.out.println("phone = " + phone + ", name = " + name);
               }
           }
           catch (Exception e)
           {
               e.printStackTrace();
           }
           finally
           {
               /* clean up at the end always **/
               if (resultSet != null)
               {
                   resultSet.close();
               }
               if (statement != null)
               {
                   statement.close();
               }
               if (connection != null)
               {
                   connection.close();
               }
           }
       }
   }
   ```
   {: codeblock}

   Replace the parameters in the command with the following:
   `<PRESTO_URL>` Identifies the jdbc URL to the Presto server.
   `<EMAIL_ID>` with your email ID
   `<API_KEY>` with the API key

   If you are using IBM IAM token, replace `ibmapikey` with `ibmlhtoken` and pass the token.
   {: note}

6. Compile and run the command.

## Connecting to Presto engine using Python scripts
{: #conn-to-prestpython}

1. Install python 3.x (3.10 or later recommended) and `pip3` on your client workstation.

2. Use the DBAPI interface to query Presto. Following is a sample python script.

   ```bash
   import os
   import prestodb
   username=os.environ["ENG_USERNAME"]
   password=os.environ["ENG_PASSWORD"]
   hostname=os.environ["ENG_HOST"]
   portnumber=os.environ["ENG_PORT"]
      with prestodb.dbapi.connect(
      host=hostname,
      port=portnumber,
      user=username,
      catalog='tpch',
      schema='tiny',
      http_scheme='https',
      auth=prestodb.auth.BasicAuthentication(username,password)
      ) as conn:
   cur = conn.cursor()
   cur.execute('select * from tpch.tiny.customer limit 10')
   rows = cur.fetchall()
   print(rows)

   ```
   {: codeblock}

   The command queries the `system.runtime.nodes` system tables that show the nodes in the Presto cluster.
   The DBAPI implementation in `prestodb.dbapi` provides methods to retrieve few rows. For example, `Cursorfetchone()` or `Cursor.fetchmany()`. By default `Cursor.fetchmany()` fetches one row. Set `prestodb.dbapi.Cursor.arraysize` accordingly.
   {: note}

4. Compile and run the command.
