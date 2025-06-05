---

copyright:
  years: 2022, 2025
lastupdated: "2025-06-05"

keywords: Spark, query, server,JDBC, Driver

subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Connecting to Spark query server by using Spark JDBC Driver
{: #dbt_watsonx_connt}


You can connect to the Spark query server in the following ways and execute queries to analyze your data.

* [Using DBeaver (JDBC clients)](#dbt_dbvr)
* [Using Java (JDBC Client) code](#dbt_java)
* [Using Python (PyHive JDBC Client)](#dbt_dbvr_Pyth)

## Before you begin
{: #dbt_watsonx_c_bfb}

1. Install watsonx.data.
1. Provision native Spark engine in watsonx.data.
1. JDBC Driver: `queryserver-jdbc-4.1.0-SNAPSHOT-standalone.jar`.
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
   1. Provide the JDBC URL using the following format : `jdbc:hive2://<HOST>/default;lhInstanceId=<INSTANCE>;httpPath=<URI>`.
   1. Select **Authentication**, provide **Username** as your username and your IAM API key as the password.
   1. **Save** and connect to the connection by double-clicking.


## Connecting to Spark query server by using Java (JDBC Client) code
{: #dbt_java}

Ensure your Java CLASSPATH includes the downloaded JDBC driver. For example:

`java -cp queryserver-jdbc-4.1.0-SNAPSHOT-standalone.jar MyExampleJDBC.java`

You can specify the following parameters and use the following Java code to connect to the Spark query server.

```bash
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

public class MyExampleJDBC {
    public static void main(String[] args) throws Exception {
        // SaaS ONLY
        String host = "HOST-WITHOUT-PROTOCOL";
        String instance = "INSTANCE";
        String uri = "URI OF QUERY SERVER";
        String user = "YOUR-EMAIL";
        String apikey = "IAM-API-KEY";

        String jdbcUrl = String.format("jdbc:hive2://%s/default;lhInstanceId=%s;httpPath=%s;", host, instance, uri);

        try {
            // Load the Hive JDBC driver
            Class.forName("com.ibm.wxd.spark.jdbc.QueryServerDriver");

            // Connect to Hive
            Connection con = DriverManager.getConnection(jdbcUrl, user, apikey);
            Statement stmt = con.createStatement();

            System.out.println("Connected");

            // Sample query
            String sql = "show databases";
            ResultSet rs = stmt.executeQuery(sql);

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
}
```
{: .codeblock}

## Connecting to Spark query server by using Python (PyHive JDBC Client)
{: #dbt_dbvr_Pyth}

To connect to the Spark query server using a Python program, do the following:
