---

copyright:
  years: 2022, 2024
lastupdated: "2024-04-30"

keywords: watsonxdata, watsonx.data, presto, jdbc client, cloud

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

# Connecting to Presto server using Java JDBC
{: #con-presto-cloud-jdbc}

Presto CLI provides a terminal-based interactive shell to run queries.
{: shortdesc}

Complete the following steps to connect to Presto engine in {{site.data.keyword.lakehouse_full}} instance on {{site.data.keyword.cloud_notm}} through a JDBC Java client or application.

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
{: #conn-to-prestoeng1}

1. Download and install the [latest JDBC drivers](https://prestodb.io/docs/current/installation/jdbc.html) on the client machine.

2. Add the downloaded `jar` file to the class path of your Java application.

3. Create a Java application by using JDBC interface. Following is an example for PrestoJdbcSample.Java:

   ```bash
   import java.sql.*;
   import java.util.Properties;
   public class PrestoJdbcSample {
   public static void main(String[] args) {
   try {
   String url = "<PRESTO_URL>/tpch/sf1?SSL=true"
   String driverClass = "com.facebook.presto.jdbc.PrestoDriver";
   Class.forName(driverClass);
   Properties properties = new Properties();
   properties.setProperty("user", "ibmapikey_<EMAIL_ID>");
   properties.setProperty("password", "<API_KEY>");
   Connection connection = DriverManager.  getConnection(url, properties);
   String query = "SELECT * FROM customer LIMIT 10";
   Statement statement = connection.createStatement();
   ResultSet resultSet = statement.executeQuery(query);
   while (resultSet.next()) {
   // Get the values from the current row
   String phone = resultSet.getString("phone");
   String name = resultSet.getString("name");
   System.out.println("phone = " + phone + ", name = " + name);
   resultSet.close();
   statement.close();
   connection.close();
   } catch (Exception e) {
   e.printStackTrace();
   }
   }
   }
   ```
   {: codeblock}

   Replace the parameters in the command with the following:
   `<PRESTO_URL>` with Presto JDBC URL
   `<EMAIL_ID>` with your email ID
   `<API_KEY>` with the API key that you downloaded from IBM Cloud.
   If you are using IBM IAM token, replace `ibmapikey` with `ibmiamtoken` and pass the token.
   {: note}

4. Compile and run the command.
